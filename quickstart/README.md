# Quickstart

> This document allows developers to learn quickly. If you need detailed documentation, please read the <storng>API reference.</strong>

> In this document, you will most likely need to adjust the command line with different versions of Python.

Who is suitable to read this document?

* Have very solid Python foundation and development experience.
* Understand the basic HTTP protocol.
* Very skilled GIT.

What kind of environment is needed?

* Python 3.5 +
* Nginx 1.19.3 + (In production)

## Install

Create a development environment:

``` bash
$ mkdir ibuprofen-project
$ cd ibuprofen-project
$ python3 -m venv venv
```

Use package manager to install and update:

``` bash
$ pip install -U ibuprofen
```

You can also download the latest version of GitHub via GIT:

``` bash
$ git clone https://github.com/isclub/ibuprofen
$ cd ibuprofen
$ python setup.py install
```

## Application

With code like this, you can create a web application object:

``` python
from ibuprofen import Ibuprofen

app = Ibuprofen(
    runtime_name=__name__
)
```

The code above creates a minimal web application object with which most of the work is done.

## Running

Run the service through the `run()` function, which calls Python's default WSGI server to run.

``` python
from ibuprofen import Ibuprofen

# Start Ibuprofen
app = Ibuprofen(
    runtime_name=__name__
)

# Run WSGI Server
if __name__ == "__main__":
    app.run()
```

Now, open it through a browser `localhost:8080`  To access your web application, but in fact, you'll see a 404 error interface because you haven't done anything yet.

``` bash
The Ibuprofen Running at http://127.0.0.1:8080/
127.0.0.1 - - [23/Oct/2020 20:14:08] "GET / HTTP/1.1" 404 13
127.0.0.1 - - [23/Oct/2020 20:14:09] "GET /favicon.ico HTTP/1.1" 404 13
```

You can adjust the running port of the web application by changing the `port` parameter. Like this:

``` python
from ibuprofen import Ibuprofen

# Start Ibuprofen
app = Ibuprofen(
    runtime_name=__name__
)

# Run WSGI Server
if __name__ == "__main__":
    app.run(port=5000)
```

Now your web application is running on the local port `5000`.

## Route

You can respond to client requests by adding routes. Like this:

``` python
@app.make_route("/")
def hello(context):
    return context.Response("Hello")


@app.make_route("/hello")
def hello(context):
    return context.Response("Hello")
```

You can now use a browser to access the interface with URL `/` or `/hello`, and you will see your text.