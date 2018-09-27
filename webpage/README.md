# Q&A List for the Issues in Webpage

## 1. Javascipt for Data Visualization with ZingCharts / HighCharts / Q3
### Q1.1 How can I recieve the data from flask for javascript loading?

A1.1 The answer is divided into two parts according the types of data

1. String data
	+ Take the ZingCharts.js as an example. The string value or list should be loaded with ```{{data.stringName | tojson}}```, 
	because if you don't use ```tojson```, the ```""``` and ```''``` can not be converted correctly, and this causes the string data can't be loaded.
2. Numaric data
	+ The numaric data can be used directly with ```{{data.numaricDataName}}```

- - - 
### Q1.2 How can I use the data in the javascript?

A1.2 Before you use the data, it can be better that you check whether the data exists or not. You can use
```html
{% if data %}
	<!-- Place your javascript here-->
{% else %}
	<!-- If data does not exist, what do the script gonna do?-->
{% endif %}
```
And then, if the data that the javascript needs exist, you could use these methods for data loading in this.

1. String data
	+ When you load the string data correctly with the method mentioned in the A1.1, you can use the string directly.

```java
        var stringData = {{ data.stringName | tojson }}
        var myChart = {
                "scale-x": {
                    "values": stringData,
                }
            }
```

2. Numeric data
	+ Take barplot of the ZingCharts as an example. 
	If the series data is the value of barplot, you should prepare the numeric data as a list series. And then,
```java
        var myChart = {
                "series": [{
                    "values": {{ data.numaricDataName }}
                }]
            }
```

3. Convert the numeric data into string
	+ For example, sometimes, the charts need to show labels according to the numaric value. 
	And we should convert the numeric values into strings.
```java
		// This is a label with rules
        var myChart = {
        	    "plot": {
                    "tooltip": {
                        "rules": [{ //Rule 1
                            "rule": "%v < "+String({{data.threshold}}) ,
                            "text": "%data-sub-text is<br>less than"+String({{data.threshold}}),
                        }, { //Rule 2
                            "rule": "%v >= "+String({{data.threshold}}),
                            "text": "%data-sub-text is<br> larger than"+String({{data.threshold}}),
                        }],
                    },
                }
            }
```

- - - 

### Q1.3 __Barplot of ZingChart:__ How do a certain bar show its x ticklabel name, y ticklabel value or series type?

A1.3 The answer goes from an easier one:

1. y ticklabel value: ```%v``` - means the ```values``` in ```series```.
2. Series type: ```%t``` - means the ```text``` in ```series```.
3. x ticklabel name:
	+ You should set a name list of a certain data series,
```java
        var myChart = {
                "series": [{
                    "values": {{ data.numeric }},
                    "text": "Series-1",
                    "data-sub-text": nameStringList
                    // This nameString list is loaded by the | tojson
                }]
            }
```
And then, you could find the ```data-sub-text``` of a certain bar with the expression```%data-sub-text```.

## 2. Structure the Templates with the Help of  Jinja

## 3. Layout / CSS Issues








