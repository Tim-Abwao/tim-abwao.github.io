---
tags: web-apps flask
last_modified_at: 2021-01-24T13:40:00+03:00
---
[Flask][1] is a "*lightweight... web app framework*" in Python. It is designed to be *simple* & *basic*; making it easy to learn, while simultaneously allowing experienced web developers the freedom to integrate the tools they prefer.

![Flask logo][2]

## Installation

*Flask* can be installed using `pip`:

```bash
pip install Flask
```

The *Flask* [installation guide][3] outlines how to:

- work in a *virtual environment*

  ```bash
  python3 -m venv venv
  source venv/bin/activate
  pip install Flask
  ```

- install the latest *unreleased* version

  ```bash
  pip install -U https://github.com/pallets/flask/archive/master.tar.gz
  ```

- include [optional dependencies][4] to enhance functionality.

## Getting Started

The *Flask* [Quickstart guide][5] wonderfully introduces its main features:

- Creating and running web apps
- Routing & URL building
- Including static assets
- Rendering HTML templates
- Handling HTTP requests, among others.

A simple *Flask* app looks something like this:

```python
from flask import Flask
app = Flask(__name__)


@app.route('/')
def hello_world():
    return 'Hello, World!'
```

The app is essentially an instance of the [`Flask` class][21], and the `route()` decorator provides a convenient way to bind view functions to URLs. Please refer to the [minimal application][22] explanation for more details.

To run the above app, save the code as a file, for instance *myapp.py*. Then use the following commands to launch the [Flask development server][9]:

```bash
export FLASK_APP=myapp
export FLASK_ENV=development
flask run
```

By default, it will be running locally at port 5000. If you browse to <http://127.0.0.1:5000/>, you should see the text "Hello, World!".

![Flask app running][10]

[*Flask*'s tutorial][6] provides a step-by-step guide to building a basic blog in which users can register, log in, and create, edit or delete posts. It also describes how to package the blog for distribution.

If you're completely new to web development, [MDN's Learn Web Development][7] and [W3Schools][8] could quickly bring you up to speed. *Flask* can be used to make wonderful, dynamic websites and apps; but this would require some understanding of HTML, CSS and JavaScript.

## Building a Basic Flask App

You can structure a *Flask* app as a *module*, or as a *package* as shown below:

```md
  As a module                       As a Package
  -----------                       ------------
  ├── static                        └── basic_flask_app
  |   ├── style.css                     ├── __init__.py
  |   └── fruits.jpg                    ├── static
  ├── templates                         |   ├── style.css
  |   └── fruits.html                   |   └── fruits.jpg
  └── basic-flask-app.py                ├── templates
                                        |   └── fruits.html
                                        └── app.py
```

For this demo, we'll be using the module layout. The code for this entire project is available [here][18].

### 1. Install *Flask* in a virtual environment

First, create a folder to work in:

```bash
mkdir my-flask-app
cd my-flask-app
```

Afterwards, create a virtual environment and install *Flask*:

```bash
python3 -m venv venv
source venv/bin/activate
pip install -U pip
pip install Flask
```

### 2. Create the app script

Here's the complete Python script for this demo app:

```python
from flask import Flask, render_template, request, redirect, url_for


app = Flask(__name__)

fruits = ["Mangoes", "Apples", "Cherries", "Strawberries", "Pears"]

@app.route('/')
def index():
    return render_template("fruits.html", title="ACME Fruit Store",
                           fruit_list=fruits)


@app.route('/checkout', methods=["GET", "POST"])
def checkout():
    if request.method == 'POST':
        basket = []
        for item in fruits:
            try:
                basket.append(request.form[item])
            except KeyError:
                pass
        if not basket:
            basket = ['No fruits selected.']
        return render_template('fruits.html', selection = basket)

    return redirect(url_for('index'))


if __name__ == '__main__':
    app.run()
```

The app consists of two web pages:

- The home page ('/') which contains a form to select fruits.
- A checkout page ('/checkout') that just extracts and displays data submitted from the form in the home page.

You'll need to save the script as a file e.g. *basic-flask-app.py*.

Data from HTML forms is accessible through *Flask*'s [request object][16]. For instance:

```python
request.method  # gives the current HTTP method ('GET', 'POST','PUT', ...)
request.form  # gives the form data as a dictionary
request.form['Key']  # gets data from the element named 'Key'
```

Form data from POST requests is commonly handled thusly:

```python
@app.route('/some_url', methods=["GET", "POST"])
def some_url():
    if request.method == 'POST':
    # Extract and process the form data
```

### 3. Collect static assets

In order for *Flask* to serve CSS, JavaScript, or image files saved locally; they'll need to be placed in a [static folder][11] (**/static** by default). This makes them accessible at the URL "*/static*", and via *Flask*'s [url_for()][12] method:

```python
url_for('static', filename="style.css")
```

Below is a sample CSS style-sheet. You could save it (or write your own if you wish) as a file named *style.css* in the *static* folder.

```css
body {
    margin: 5%;
    font-size: 1.5em;
}
```

### 4. Add an HTML template

Writing code for entire webpages within the app's Python scripts could get messy, fast. *Flask* offers a fitting solution: the [Jinja2 HTML templating engine][13]. *Jinja* supports variables, conditionals and iteration, enabling it to efficiently implement complex workflows while avoiding needless repetition.

Sample *Jinja* syntax:

```{% raw %}
{% if condition %} action {% endif %}  <!-- an if statement -->
{% for iterable %} action {% endfor %}  <!-- a for loop -->
{{ name }}  <!-- to print the variable 'name' to the template output -->
{# ... #}  <!-- for comments, not included in the template output -->{% endraw %}
```

Templates to be rendered need only be placed in the [templates folder][14] (**/templates** by default), and Flask's [render_template()][15] method will do the rest.

Here's a sample *Jinja* template:

```html
<!DOCTYPE html>
<html>

<head>
  <link rel="stylesheet" type="text/css" href="{%raw%}{{ url_for('static', filename='style.css')}}{%endraw%}">
  <title>{%raw%}{{ title }}{%endraw%}</title>
  <style>
    body  {
      background: center / cover url("{%raw%}{{ url_for('static', filename='fruits.jpg') }}{%endraw%}");
    }
  </style>
</head>

<body>
  {%raw%}{% if fruit_list %}{%endraw%}
  <h1> Please select: </h1>
  <form action="{%raw%}{{ url_for('checkout')}}{%endraw%}" method="POST">
    <ul>
      {%raw%}{% for fruit in fruit_list %}{%endraw%}
      {%raw%}{{ fruit }}{%endraw%}<input type="checkbox" value="{%raw%}{{ fruit }}{%endraw%}" name="{%raw%}{{ fruit }}{%endraw%}"><br>
      {%raw%}{% endfor %}{%endraw%}
    </ul>
    <input type="submit">
  </form>
  {%raw%}{% endif %}{%endraw%}

  {%raw%}{% if selection %}{%endraw%}
  <h2>Selected fruits:</h2>
  <ul>
    {%raw%}{% for item in selection %}{%endraw%}<li>{%raw%}{{ item }}{%endraw%}</li>{%raw%}{% endfor %}{%endraw%}
  </ul>

  <a href="{%raw%}{{ url_for('index') }}{%endraw%}"> Back to home</a>
  {%raw%}{% endif %}{%endraw%}
</body>

</html>
```

You'll need to save it as a file e.g. *fruits.html* in the *templates* folder.

The background image referenced in the template above can be found [here][23]. (The original photo, by [ja ma][24] can be found [here][25])

### 5. Conclusion

Once you have all the necessary files appropriately positioned, you can launch the demo *Flask* app using the commands:

```bash
export FLASK_APP=basic-flask-app
export FLASK_ENV=development
flask run
```

Result:

![ACME groceries webpage][17]

## Next Steps

*Flask* offers a number of [deployment options][19]. If you'd like to challenge yourself; try coming up with a great idea for a web app, build it, and then deploy it on [Heroku][20] - a popular choice.

[1]: https://flask.palletsprojects.com/en/1.1.x/
[2]: /assets/images/articles/flask-webapp/logo-full.svg
[3]: https://flask.palletsprojects.com/en/1.1.x/installation
[4]: https://flask.palletsprojects.com/en/1.1.x/installation/#optional-dependencies
[5]: https://flask.palletsprojects.com/en/1.1.x/quickstart
[6]: https://flask.palletsprojects.com/en/1.1.x/tutorial
[7]: https://developer.mozilla.org/en-US/docs/Learn
[8]: https://www.w3schools.com
[9]: https://flask.palletsprojects.com/en/1.1.x/server/
[10]: /assets/images/articles/flask-webapp/flaskrun.png
[11]: https://flask.palletsprojects.com/en/1.1.x/api/#flask.Flask.static_folder
[12]: https://flask.palletsprojects.com/en/1.1.x/quickstart/#url-building
[13]: https://jinja.palletsprojects.com/en/2.11.x/
[14]: https://flask.palletsprojects.com/en/1.1.x/api/#flask.Flask.template_folder
[15]: https://flask.palletsprojects.com/en/1.1.x/api/#flask.render_template
[16]: https://flask.palletsprojects.com/en/1.1.x/api/#flask.request
[17]: /assets/images/articles/flask-webapp/flask-demo.gif
[18]: https://github.com/Tim-Abwao/blog-projects/tree/master/basic-flask-app
[19]: https://flask.palletsprojects.com/en/1.1.x/deploying/
[20]: https://devcenter.heroku.com/articles/getting-started-with-python?singlepage=true
[21]: https://flask.palletsprojects.com/en/1.1.x/api/#flask.Flask
[22]: https://flask.palletsprojects.com/en/1.1.x/quickstart/#a-minimal-application
[23]: https://github.com/Tim-Abwao/blog-projects/blob/master/basic-flask-app/static/fruits.jpg
[24]: https://unsplash.com/@ja_ma
[25]: https://unsplash.com/photos/-gOUx23DNks
