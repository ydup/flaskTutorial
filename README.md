# Flask + Python + Webpage Tutorial for Beginners

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
+ The CSS, javascipt and image files locate in the folder named _static_. The path of css, js and image should be _static/_. Don't write the path as _../static_, because flask can't find them.

And then, if you have many wabpages to handle, and some of them use a same template, such as header and footer, 
you can structure them into this, with the help of Jinja2:

Template:
```html
<!DOCTYPE html>
<!-- This is header-->
<!-- Common field-->
<!-- Body block start -->
{% block body %}
{% endblock %}
<!-- Body block end-->
<!-- This is footer-->
```
A specific webpage:
```html
<!DOCTYPE html>
<!-- You don't need to write the header here-->
<!-- Body block start -->
{% block body %}
<!-- Place body here-->
{% endblock %}
<!-- Body block end-->
<!-- You don't need to write the footer here-->

```
And this chapter is a brief introduction to the structure of webpages. The methods how webpages and server communicate will be shown in the next chapter.

## 5. How does the server communicate with webpages

### 5.1 Access the Webpages
We have the webpages in the chapter 4, and the first thing you gonna ask must be how I can access the webpage, even more, how I can shift different webpages manually or automatically.
Before this, you should get to learn the ```@app.route```.

main.py to access a webpage:
```python
app = Flask(__name__)
 # Basic part of the html
@app.route('/')
@app.route('/into')
def intro():
	return render_template('intro.html')
```

```@app.route``` helps the server detect the actions such as click or redirect and trigger the decorated functions.
You could use many paths to access a certain webpage, such as the route '/' and '/into' that link to a same webpage "intro.html".
And in the html, you just need to write this. And when the server is started or the href is clicked, the function ```intro()``` will be triggered.

```html
<a href="into"></a>
```

### 5.2 Receive Data Uploaded From the Webpages
Post and get methods help webpage communicate with server. In this section, we introduce how the server receive data from webpages.

main.py
```python
# Upload file from data.html
@app.route('/uploader', methods=['GET', 'POST'])
def upload_file():
	if request.method == 'POST':
		f =request.files['file']
		f.save(secure_filename(f.filename))
		return render_template('data.html', name=f.filename)
```

data.html - body
```html
{% if name %}
<h1 class="mb-10">{{name}} Data Loaded</h1>
{% else %}
<h1 class="mb-10">Please Upload Data</h1>
{%endif%}
```
The keyword ```name``` can be changed to ```f.filename``` when the data file is uploaded to the server.

data.html - form
```html
<form action = "uploader" method = "POST" enctype = "multipart/form-data">
<input type = "file" name = "file"/>
<input type = "submit" value="Submit"/>
</form>	
```
The ```form``` part creates a interface for user to upload local file.


### 5.3 Server Send Data to the Webpages
In this section, we introduce how the server send data to webpages.
main.py
```python
# Upload file from data.html and send data as json to webpages
@app.route('/uploader', methods=['GET', 'POST'])
def upload_file():
	if request.method == 'POST':
		f =request.files['file']
		f.save(secure_filename(f.filename))
		# Read the data file
		df = pd.read_csv(f.filename)
		chart_data = df.to_dict(orient='records')
		# Sent the data as a json file
		chart_data = json.dumps(chart_data, indent=2)
		data = {'chart_data': chart_data}
		return render_template('data.html', name=f.filename, data=data)
```
And you could write a javascipt to receive the json data from server.












