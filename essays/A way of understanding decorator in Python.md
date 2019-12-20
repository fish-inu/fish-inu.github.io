---
layout: essay
type: essay
title: A way of understanding decorator in Python
# All dates must be YYYY-MM-DD format!
date: 2019-10-23
labels:
  - Python
  - Decorator
---

Life is short, use Python. Python is easy to learn for newbies like me who desire both functionality and performance without complex logic, until **advanced** concepts come in front of us including asynchronous programming, descriptor, decorator, among many others. 

Admittedly, I have used these advanced features in the way of importing those awesome open source packages, but I didn't type them very much myself. It's OK to only import packages because we just want functionality and retrieve results without wasting time. Beyond these basic needs, however, we sometimes also need to write the same function as the one from certain awesome package for the purpose of learning to deepen our understanding of  programming principles behind these interfaces.

Let's jump right into the theme of today, decorator.

Let's take an example when we don't use decorator. There are times when you make a request for response from remote server but failed because your connection to network is not stable. So you might try, say, twice more.

```python
for i in range(1,4):
    try:
        request_something()
    except:
    	print('Bite the dust!') # try again
        continue
    else:
        break       
else:
	print('Killer Queen failed to do that') # we failed after 3 attempts
```

This will try 3 times when `request_something()` failed and print a message when it all failed. If you are a fan of jojo you would get point of these messages but you can just pay attention to the comments if you are not. 

But this code block is not good enough in that we have to duplicate the code around `request_something` whenever we make another request.

Decorator comes to rescue. In this case, we focus on one of its characteristic, reusability. Decorator comes in handy when you are going to modify your definition of a particular function. 

Consider the following example:

```python
def retry(request_sth):
    def wrapper():
        for i in range(1,4):
            try:
                request_sth()
            except:
                print('Bite the dust!') # try again
                continue
            else:
                break       
        else:
            print('Killer Queen failed to do that') # we failed after 3 attempts
	return wrapper            
```

It would be much clearer if we use `diff` to see what changes are made:

```diff
+ def retry(request_sth):
+    def wrapper():
     	for i in range(1,4):
            try:
                request_sth()
            except:
                print('Bite the dust!') # try again
                continue
            else:
                break       
        else:
            print('Killer Queen failed to do that') # we failed after 3 attempts
+    	return wrapper 
```



To summarize these changes:

- We define a new function called `retry` and pass in a function, in this case, `request_sth`.
  - It allows to use `@retry` syntax to modify a function. 
- We define inner function `wrapper` and return it. 
  - Why bother? We will talk about it soon.
- The rest of code is the same as  the first code block in this post.

To answer why we define a inner function, we can just test it:

```diff
def retry(request_sth):
-    def wrapper():
     	for i in range(1,4):
            try:
                request_sth()
            except:
                print('Bite the dust!') # try again
                continue
            else:
                break       
        else:
            print('Killer Queen failed to do that') # we failed after 3 attempts
-    	return wrapper 
+ @retry
+ def request_sth():
+	import requests
+	response = requests.get(<url>)

request_sth()
```

After you run it, it will work as expected until we hit line 19 `request_sth()`, it will raise an error. The code would run normally If we didn't remove these lines I marked as red. Why?

Under the hood, to put it simply, when we hit line 14, an invisible line is executed: `request_sth = retry(request_sth)`. If you want to dive deeper into it, I recommend checking out `Simple Decorator ` section from an awesome article [Primer on Python Decorators](https://realpython.com/primer-on-python-decorators/).

Reminder: Some lines in code block might not indent properly in `diff` view.
