---
tags: web-apps flask
last_modified_at: 2021-11-06T12:57:00+03:00
---
[Flask][flask] is a "*lightweight... web app framework*" in Python. It is designed to be *simple* & *basic*; making it easy to learn, while simultaneously allowing experienced web developers the freedom to integrate the tools they prefer.

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
- Handling HTTP requests, among others.

There's also a [*Flask* tutorial][flask-tutorial], which walks you through how to build a basic blog that allows user registration, log in, and the creation / modification / deletion of posts.

If you're completely new to web development, there are numerous online resources (e.g. [MDN's Learn Web Development][mdn-learn], [W3Schools][w3schools], etc) that could quickly bring you up to speed.

## Building a Basic Flask App

We'll structure the app as shown below:

```md
├── app.py
├── static
│   ├── fruits.jpg
│   └── style.css
└── templates
    └── fruits.html
```

### 1. Install *Flask*

Create a folder to work in:

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

### 2. Create the app files

I'd recommend doing this in your favourite text editor or IDE.

#### 2.1 `app.py`

```python
from flask import Flask, render_template, request, redirect, url_for


app = Flask(__name__)

fruits = ["Mangoes", "Apples", "Cherries", "Strawberries", "Pears"]


@app.route("/")
def index():
    return render_template(
        "fruits.html", title="ACME Fruit Store", fruit_list=fruits
    )


@app.route("/checkout", methods=["GET", "POST"])
def checkout():
    if request.method == "POST":
        basket = request.form.getlist("fruit")

        if not basket:
            basket = ["No fruits selected."]

        return render_template("fruits.html", selection=basket)

    return redirect(url_for("index"))


if __name__ == "__main__":
    app.run(debug=True)
```

This defines:

- A home(*index*) page ('/'), which contains a form to select fruits.
- A *checkout* page ('/checkout') that just extracts and displays data submitted from the form in the home page.

#### 2.2 `static/fruits.jpg`

[Download from here][app-background]. (The original photo, by [@ja ma][@ja ma], can be found [here][unsplash-img-link])

> **NOTE:** In order for *Flask* to serve CSS, JavaScript, or image files saved locally; they'll need to be placed in a [static folder][static-folder].

#### 2.3 `static/style.css`

```css
body {
    background: center / cover url("/static/fruits.jpg");
    font-size: 1.4em;
    margin: 5% auto;
    width: 80%;
}
```

#### 2.4 `templates/fruits.html`

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

  <a href="{%raw%}{{ url_for('index') }}{%endraw%}"> Back to home</a>
  {%raw%}{%endif %}{%endraw%}
</body>

</html>
```

> **NOTE:** Templates to be rendered need to be placed in the [templates folder][templates-folder].

### 3. Running the app

Once all the necessary files are in position, you can launch the *Flask* app using the commands:

```bash
export FLASK_ENV=development  # to enable debug mode
flask run
```

Check out the [*Flask* Command Line Interface][flask-cli] for more details.

Result:

![ACME groceries webpage][app-screencast]

The code for the [complete app is available here][github-link]

## Next Steps

*Flask* offers a number of [deployment options][flask-deploy]. You could try coming up with a great idea for a web app, build it, and then deploy it on [Heroku][heroku] - a popular choice.

[flask]: https://flask.palletsprojects.com/
[flask-logo]: /assets/images/articles/flask-webapp/logo-full.svg
[flask-install]: https://flask.palletsprojects.com/en/2.0.x/installation/
[flask-quickstart]: https://flask.palletsprojects.com/en/2.0.x/quickstart/
[flask-tutorial]: https://flask.palletsprojects.com/en/2.0.x/tutorial
[flask-cli]: https://flask.palletsprojects.com/en/2.0.x/cli/
[flask-deploy]: https://flask.palletsprojects.com/en/2.0.x/deploying/
[app-background]: https://raw.githubusercontent.com/Tim-Abwao/blog-projects/main/basic-flask-app/static/fruits.jpg
[mdn-learn]: https://developer.mozilla.org/en-US/docs/Learn
[w3schools]: https://www.w3schools.com
[static-folder]: https://flask.palletsprojects.com/en/2.0.x/api/#flask.Flask.static_folder
[templates-folder]: https://flask.palletsprojects.com/en/2.0.x/api/#flask.Flask.template_folder
[app-screencast]: /assets/images/articles/flask-webapp/flask-demo.gif
[github-link]: https://github.com/Tim-Abwao/blog-projects/tree/main/basic-flask-app
[heroku]: https://devcenter.heroku.com/articles/getting-started-with-python?singlepage=true
[@ja ma]: https://unsplash.com/@ja_ma
[unsplash-img-link]: https://unsplash.com/photos/-gOUx23DNks
