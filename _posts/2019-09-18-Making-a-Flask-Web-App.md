---
description: Beginners guide on building a basic Flask web app.
tags: web-apps flask
last_modified_at: 2022-07-05T15:52:00+03:00
---
[Flask][flask] is a "*lightweight... web app framework*" in Python. It is designed to be [simple but extensible][micro]; making it easy to learn, while simultaneously allowing experienced web developers the freedom to integrate the tools they prefer.

![Flask logo][flask-logo]

## Installation

*Flask* can be installed using `pip`:

```bash
pip install Flask
```

The *Flask* [installation guide][flask-install] has more details on how to:

- work in a *virtual environment*
- install the latest *unreleased* version
- include *optional dependencies* to enhance functionality.

## Getting Started

The *Flask* [Quickstart guide][flask-quickstart] wonderfully introduces its main features:

- Routing & URL building
- Including static assets
- Rendering HTML templates
- Handling HTTP requests

and much more.

There's also a [*Flask* tutorial][flask-tutorial], which walks you through how to build a basic blog that allows user registration, log in, and the creation / modification / deletion of posts.

If you're completely new to web development, there are numerous online resources (e.g. [MDN's Learn Web Development][mdn-learn], [W3Schools][w3schools], etc) that could quickly bring you up to speed.

## Building a demo *Flask* app

To keep things simple, let's create a minimal *Flask* app that just takes user input and displays it:

![ACME groceries *Flask* app][app-screencast]

We'll need to [install *Flask* in a virtual environment][flask-venv], and then create the following files:

```md
myproject
├── app.py
├── static
│   ├── fruits.jpg
│   └── style.css
└── templates
    └── fruits.html
```

The code for the [complete app is available here][github-link].

### 1. `app.py`

Defines:

- A home page, which contains a form to select fruits.
- A checkout page that displays data submitted in the home page.

```python
from flask import Flask, render_template, request, redirect, url_for

app = Flask(__name__)
fruits = ["Mangoes", "Apples", "Cherries", "Strawberries", "Pears"]


@app.route("/")
def home() -> str:
    """Creates the home page, with a form to capture user input.

    Returns:
        str: Rendered HTML.
    """
    return render_template(
        "fruits.html", title="ACME Fruit Store", fruit_list=fruits
    )


@app.route("/checkout", methods=["GET", "POST"])
def checkout() -> str:
    """Creates the checkout page that displays user input.

    Returns:
        str: Rendered HTML.
    """
    if request.method == "POST":
        basket = request.form.getlist("fruit") or ["No fruits selected."]

        return render_template("fruits.html", selection=basket)

    return redirect(url_for("home"))


if __name__ == "__main__":
    app.run(debug=True)
```

### 2. `static/fruits.jpg`

The background image, [available here][app-background] (The original photograph, by [@ja ma][@ja ma], can be found [here][unsplash-img-link]).

> **NOTE:** In order for *Flask* to serve CSS, JavaScript, or image files stored locally; they'll need to be placed in a [static folder][static-folder].

### 3. `static/style.css`

Sets the basic style and layout.

```css
body {
    background: center / cover url("/static/fruits.jpg");
    font-size: 1.4em;
    margin: 5% auto;
    width: 80%;
}
```

### 4. `templates/fruits.html`

Defines the app's structure.

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" type="text/css" href="{%raw%}{{ url_for('static', filename='style.css')}}{%endraw%}">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>{%raw%}{{ title }}{%endraw%}</title>
</head>
<body>
  {%raw%}{%if fruit_list %}{%endraw%}
  <h1> Demo Flask App</h1>
  <h2>Please Select:</h2>
  <form action="{%raw%}{{ url_for('checkout')}}{%endraw%}" method="POST">
    <ul>
      {%raw%}{%for fruit in fruit_list %}{%endraw%}
      {%raw%}{{ fruit }}{%endraw%}<input type="checkbox" value="{%raw%}{{ fruit }}{%endraw%}" name="fruit"><br>
      {%raw%}{%endfor %}{%endraw%}
    </ul>
    <input type="submit">
  </form>
  {%raw%}{%endif %}{%endraw%}

  {%raw%}{%if selection %}{%endraw%}
  <h2>Selected fruits:</h2>
  <ul>
    {%raw%}{%for item in selection %}{%endraw%}
    <li>{%raw%}{{ item }}{%endraw%}</li>
    {%raw%}{%endfor %}{%endraw%}
  </ul>

  <a href="{%raw%}{{ url_for('home') }}{%endraw%}"> Back to home</a>
  {%raw%}{%endif %}{%endraw%}
</body>
</html>
```

> **NOTE:** Templates to be rendered need to be placed in the [templates folder][templates-folder].

## Running the demo app

Once all the necessary files are in position, you can launch the app in the [command line interface][flask-cli], e.g with [*Bash*][bash]:

```bash
export FLASK_ENV=development  # to enable debug mode
flask run
```

Afterwards, navigate your browser to <http://127.0.0.1:5000> to interact with the app.

## Next Steps

*Flask* offers a number of [deployment options][flask-deploy]. You could try coming up with a great idea for a web app, build it, and then deploy it.

[flask]: https://flask.palletsprojects.com/
[micro]: https://flask.palletsprojects.com/en/2.1.x/foreword/#what-does-micro-mean
[flask-logo]: /assets/images/articles/flask-webapp/logo-full.svg
[flask-install]: https://flask.palletsprojects.com/en/2.1.x/installation/
[flask-venv]: https://flask.palletsprojects.com/en/2.1.x/installation/#virtual-environments
[flask-quickstart]: https://flask.palletsprojects.com/en/2.1.x/quickstart/
[flask-tutorial]: https://flask.palletsprojects.com/en/2.1.x/tutorial
[flask-cli]: https://flask.palletsprojects.com/en/2.1.x/cli/
[bash]: https://www.gnu.org/software/bash/
[flask-deploy]: https://flask.palletsprojects.com/en/2.1.x/deploying/
[app-background]: https://raw.githubusercontent.com/Tim-Abwao/blog-projects/main/myproject/static/fruits.jpg
[mdn-learn]: https://developer.mozilla.org/en-US/docs/Learn
[w3schools]: https://www.w3schools.com
[static-folder]: https://flask.palletsprojects.com/en/2.1.x/api/#flask.Flask.static_folder
[templates-folder]: https://flask.palletsprojects.com/en/2.1.x/api/#flask.Flask.template_folder
[app-screencast]: /assets/images/articles/flask-webapp/flask-demo.gif
[github-link]: https://github.com/Tim-Abwao/blog-projects/tree/main/basic-flask-app
[@ja ma]: https://unsplash.com/@ja_ma
[unsplash-img-link]: https://unsplash.com/photos/-gOUx23DNks
