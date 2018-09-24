# Flask + Python + Website Tutorial for Beginners

Author: Yadong Zhang
Date: 2018-09-24

This is a tutorial for beginners. But it assumes that you are familiar with python and the basic knowledge about the website.
If not, pls go to the documents of them. You don't need to be professional but have to know how to work with them.

This tutorial would focus on how to build a interactive website with the flask.
It can't be very detailed in all the features, but it will give beginners a good direction and answer your basic but essential problems.

## 1. Build with Virtualenv

When you develop different projects, you gonna use many kinds of packages. 
The virtualenv can help you built the project with all the related site-packeges in a virtual envirament.
In another word, you would develop the projects in different python enviraments, and while one is running, it does not affect 
the others.

Install the virtualenv:
```
$ sudo pip install virtualenv
```
Make a project file:
```
$ mkdir myproject
$ cd myproject
$ virtualenv venv
New python executable in venv/bin/python
Installing distribute............done.
```
Activate the virtualenv:
```
$ . venv/bin/activate
```
With all of these finished, let's install the related site-packages such as flask, pandas, numpy and so on in the activated virtualenv.

## 2. Get Some Basic Knowledge about the Flask
Flask is a framework that helps you build a light but complete website. 
You can go through the official API of Flask. 
For beginners, you could build a official provided demo to get a initial knowledge about the Flask. 
But it maybe can't answer your pressing questions: so, how can I build my website not just hello world? 

Don't be worry. I assume that you have tested the offical demo. Please read on : )

## 3. Structure of the Website Project
Before answering your questions, pls let's figure out the structure of the website project: webpage(.html, .js, .css) + server(Flask) + database. (this tutorial doesn't make introduction to the database here)

The webpage is the most frequent part that we internet users access. We can read on, download files from and upload files to them.
And there are many beautiful and interactive layouts of them. We are familiar with website but not with the server. 
In short, the server can exchange data, make analyses and calculations, response to the different actions of website, and so on.

## 4. Start the Project from Webpage Firstly
This tutorial starts with the website, furthermore, the website loaded by flask.
The website loaded by flask is different with the local html file opened directly by double click. 
This can be very puzzled for beginners. Making a comparison carefully, you will realize that the latter one can't be monitored automatically and answer the basic request methods, such as post and get. 

So how does the flask load a webpage?

Firstly, let's see how the webpage is stuctured in the flask project.

+ The webpages locate in the folder named _templates_.
+ The CSS, javascipt and image files locate in the folder named _static_.






















