# Q&A List for the Issues in Flask


## Q&A-1
Q.1 How can I recieve data from website?
A.1 You could use post as the method for upload data or data file from website.
In the flask, these ways help you obtain data.
```python
if request.method == 'POST':
	# Recieve the file and save it
	fileManager = request.files['fileName']
	fileManager.save(secure_filename(fileManager.filename))
	# Get the text value from text form
	textValue = request.form.get('textName', 'Default Value')
	# Get the option value from option form
	optionValue = request.form.get('optionName', 'Default Value')
```
And in the html, you could use any kind of form, such as
```html
<form action="actionName" enctype="multipart/form-data" method="POST">
    <label for="file">Choose a file: </label>
    <input name="fileName" id="file" type="file" />
    <br>
    <label for="text">Input a value </label>
        <input  name="textName" id="text" type="text">
    <br>
    <label for="option">Set a Method:</label>
    <select name="optionName" id="option">
        <option>-Please Choose-</option>
        <option>M-1</option>
        <option>M-2</option>
    </select>
    <input type="submit" value="Submit" />
</form>
```

## Q&A-2
Q.2 How can I send data to webpage using flask?
A.2 Before you send them, please prepare all the data into a better structure, such as.

```python
def sendData():
	#... placeholder for data preparation
	data = {'item1': item1, 'item2': item2}
	return render_template('web.html', data=data)
```
And then, you could use data.itemName to get the data in the webpage.



