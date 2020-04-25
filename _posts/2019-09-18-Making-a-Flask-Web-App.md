---
layout: post
author: Abwao
last_modified_at: 2020-04-21T14:55:00+03:00
---
[Flask](https://flask.palletsprojects.com/en/1.1.x/) is a "**lightweight... web app framework**" for Python. It is designed to be **simple** and basic; thus making it easy to learn, while simultaneously allowing experienced web developers the freedom to integrate custom/preferred features.

![Flask logo](/assets/images/logo-full.svg)<br>
<sub>*Flask logo*</sub>

## Getting Started
Flask can be installed with:
```bash
$ pip install Flask
```
For detailed instructions, please see the Flask [installation guide](https://flask.palletsprojects.com/en/1.1.x/installation/#installation).

Flask's [quickstart](https://flask.palletsprojects.com/en/1.1.x/quickstart/#quickstart) wonderfully introduces its main features. It can help you get a simple web app up and running in a matter of minutes. [Flask's tutorial](https://flask.palletsprojects.com/en/1.1.x/tutorial/#tutorial) takes this a leap further with a step-by-step guide to building a blog.

Flask can make wonderful, dynamic websites and  applications; but this will require some understanding of HTML, CSS and JavaScript. [W3Schools](https://www.w3schools.com) and [Bootstrap](https://getbootstrap.com) can be a real help for absolute beginners.   

## Flask Basics
The simplest Flask app looks something like this:
```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'
if __name__ = '__main__':
    app.run()
```
To run it, copy the above code and save it in a file e.g. **myApp.py** . You can then run it in a terminal using the command:
```bash
$ python3 myApp.py
```
 
This is all covered in the Quickstart guide. By default, the flask server will be running locally at port 5000. If you browse to [localhost:5000/](http://127.0.0.1:5000/), you should see the text "Hello, World!".

To add functionality and content, [HTML templates](https://flask.palletsprojects.com/en/1.1.x/quickstart/#rendering-templates) and [static assets](https://flask.palletsprojects.com/en/1.1.x/quickstart/#static-files) like CSS and images can be directly added. 

## Next Steps
### Example: 'Statistical Distributions App'
[This](https://statistics-distributions.herokuapp.com) is a web app designed to allow users to learn basic facts about some common statistical distributions, and create samples. The code for the app, along with instructions for use are available 
[here](https://github.com/Tim-Abwao/statistical-distributions-flask). Please feel free to give it a try, and experiment with some changes.

Challenge yourself: Think of great ideas for web apps. Then pick one to start on.
