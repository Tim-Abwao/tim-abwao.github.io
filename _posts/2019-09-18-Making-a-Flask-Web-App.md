---
layout: post
author: Abwao
last_modified_at: 2020-05-13T21:05:00+03:00
---
[Flask](https://flask.palletsprojects.com/en/1.1.x/) is a "**lightweight... web app framework**" for Python. It is designed to be simple and **basic**; making it easy to learn, while simultaneously allowing experienced web developers the freedom to integrate preferred features.

![Flask logo](/assets/images/articles/logo-full.svg)<br>
<sub>*Flask logo*</sub>

## Installation

Flask can be installed with:

```bash
$ pip install Flask
```

The Flask [installation guide](https://flask.palletsprojects.com/en/1.1.x/installation/#installation) has more information on:

- working in virtual environments

```bash
$ python3 -m venv env
$ source env/bin/activate
$ pip install Flask
```

- installing the latest unreleased version

```bash
$ pip install -U https://github.com/pallets/flask/archive/master.tar.gz
```

- and optional dependencies to improve functionality.

## Getting Started

[Flask's Quickstart](https://flask.palletsprojects.com/en/1.1.x/quickstart/#quickstart) wonderfully introduces its main features:

- Creating and running a basic app
- Routing and URL building
- Including static assets
- Rendering HTML templates
- Handling HTTP requests, among others.

It can help you get a simple web app up and running in a matter of minutes. This is also what this article is meant to help you achieve.

[Flask's tutorial](https://flask.palletsprojects.com/en/1.1.x/tutorial/#tutorial) takes this a leap further, with a step-by-step guide to building a blog.

If you're completely new to web development, [MDN's Learn Web Development](https://developer.mozilla.org/en-US/docs/Learn) and [W3Schools](https://www.w3schools.com) could quickly bring you up to speed.

Flask can be used to make wonderful, dynamic websites and apps; but this requires some understanding of HTML, CSS and JavaScript.

## Building a Simple Flask App

First, install Flask. It's good practice to work in a virtual environment:

```bash
$ python3 -m venv venv
$ source venv/bin/activate
$ pip install -U pip
$ pip install Flask
```

### 1. App Structure

```md
    A                               B
As a module                    As a Package
-----------------             ---------------------
/myapp.py                     /myapp
/static                            /__init__.py
    /style.css                     /static
/templates                             /style.css
    /Fruits.html                   /templates
                                       /Fruits.html
```

### 2. Running the App

A simple Flask app looks something like this:

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run()
```

To run it, save the above code in a file (e.g. *myapp.py*), then use the command:

```bash
$ python myapp.py
```

By default, the flask server will be running locally at port 5000.

![Flask app running](/assets/images/articles/flaskrun.png)

If you browse to [localhost:5000/](http://127.0.0.1:5000/), you should see the text "Hello, World!".

### 3. Including Static Files

In order to use local CSS, JavaScript and image files in Flask apps, they'll need to be placed in the **static** folder. This makes them accessible through Flask's **url_for()** method:

```python
url_for('static', filename="style.css")
```

Create a CSS file for this app using the code below (or write your own if you wish) and save it (e.g as *style.css*), adhering to one of the app structures above.

```css
body {
    background: lime;
    margin: 5%;
}
```

### 4. Rendering Templates

Writing code for entire webpages within Python could get messy, fast. Flask offers a fitting solution: the [Jinja2 HTML templating engine](https://jinja.palletsprojects.com/en/2.11.x/).

HTML templates to be rendered need only be placed in the **templates** folder, and flask's **render_template()** method will do the rest.

The templates can contain variables and expressions to evaluate. For instance:

```{% raw %}
{% if condition %} action {% endif %}  <!-- an if statement -->
{% for iterable %} action {% endfor %}  <!-- a for loop -->
{{ name }}  <!-- to print the variable 'name' to the template output -->
{# ... #}  <!-- for comments, not included in the template output -->
{% endraw %}
```

Here's a sample template:

```html
<!doctype html>
<html>
<head>
  <link rel="stylesheet" type="text/css" href=" {% raw %}{{ url_for('static', filename='style.css')}}{% endraw %}">
  <title>{% raw %} {{ title }}{% endraw %} </title>
</head>
<body>
  <h1>{% raw %} {{ text }} {% endraw %}</h1>
    {% raw %}{% if fruits %}{% endraw %}
      <form action="{% raw %}{{ url_for('checkout')}}{% endraw %}" method="POST">
        <ul>
          {% raw %}{% for fruit in fruits %}{% endraw %}
            <li>{% raw %}{{ fruit }}{% endraw %}<input type="checkbox" value="{% raw %}{{ fruit }}{% endraw %}" name="{% raw %}{{ fruit }}{% endraw %}"><br></li>
            {% raw %}{% endfor %}{% endraw %}
        </ul>
        <input type="submit">
      </form>
    {% raw %}{% endif %}{% endraw %}

    {% raw %}{% if selection %}{% endraw %}
      <h2>Selected fruits:</h2>
      <ul>
        {% raw %}{% for item in selection %}{% endraw %}<li>{% raw %}{{ item }}{% endraw %}</li>{% raw %}{% endfor %}{% endraw %}
      </ul>
      <a href="{% raw %}{{ url_for('index') }}{% endraw %}"> Back to home</a>
    {% raw %}{% endif %}{% endraw %}
</body>
</html>
```

To use it, save it (e.g. as *Fruits.html*), adhering to the app structure of your choice.

### 5. Accessing Request Data

Data submitted from HTML forms can be accessed using Flask's **request** object. For instance:

```python
request.method  # gives the current HTTP method ('GET', 'POST','PUT', ...)
request.form  # gives the form data as a dictionary
request.form['Key']  # gets data from the element named 'Key'
```

### 6. Conclusion

After preparing all the necessary files, the final step is to modify the *myapp.py* script to integrate them into the app:

```python
from flask import Flask, render_template, request, redirect, url_for
app = Flask(__name__)

fruits=["Mangoes", "Apples", "Cherries", "Strawberries", "Pears"]
@app.route('/')
def index():
    return render_template("Fruits.html", title="ACME Fruit Store",
                           text="Select fruits:",
                           fruits=fruits)


@app.route('/checkout', methods=["GET", "POST"])
def checkout():
    if request.method == 'POST':
        basket = []
        for item in fruits:
            try:
                basket.append(request.form[item])
            except KeyError:
                pass

        return render_template('Fruits.html', selection = basket)

    return redirect(url_for('index'))
if __name__ == '__main__':
    app.run(debug=True)

```

Afterwards, restart the app.

Result:

![ACME groceries webpage](/assets/images/articles/flaskapp.png)

![ACME groceries webpage2](/assets/images/articles/flaskapp2.png)

## Next Steps

A follow-up article soon to come will cover how to deploy your flask app.

For now, challenge yourself: think of great ideas for web apps. Then pick one to start on.
