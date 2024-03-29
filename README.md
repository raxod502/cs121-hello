# Webapps Done Right

In Spring 2019, while taking CS 121: Software Development at [Harvey
Mudd College](https://www.hmc.edu/), I was asked to give a guest
lecture on webapp development. I covered:

* Sane dependency management for Python (using Pipenv)
* Building a basic webapp (using Flask)
* Deploying it to production (using Heroku)

This document is a quick reference for all of the commands I ran in my
presentation, in case viewers wanted to refer to them later.

Check out the slides
[here](https://nextcloud.intuitiveexplanations.com/s/ZzNJW26CiMFB2T4),
and a recording of the presentation
[here](https://link.intuitiveexplanations.com/cs121-hello).

## Demo: How do I use Pipenv?

Create a Git repository for my project:

    $ mkdir hello
    $ cd hello
    $ git init

Install Pipenv:

    $ brew install pipenv

Create a `Pipfile` and `Pipfile.lock` with Flask installed:

    $ pipenv install flask

Run a command (e.g. `python`) inside your virtual environment:

    $ pipenv run ...

(Tip) Update your virtual environment if you fetch a new version of
`Pipfile.lock` from GitHub:

    $ pipenv sync

(Tip) Delete your virtual environment in case it somehow gets messed
up:

    $ pipenv --rm

(Tip) See which Pythons are installed on your computer, and use a
specific one for your virtual environment:

    $ which -a python3
    $ pipenv --python /usr/local/bin/python3

## Demo: HTTP

Install HTTPie:

    $ brew install httpie

Fetch the home page of Google, showing both request and response:

    $ http GET www.google.com --verbose

Fetch the home page of Gmail instead:

    $ http GET www.google.com/mail --verbose

## Live coding: How do I use Flask?

Run my Flask server:

    $ FLASK_DEBUG=1 pipenv run flask run

Check out the home page:

    $ http --verbose GET localhost:5000

Check out the fancy HTML page:

    $ http --verbose GET localhost:5000/fancy

## Live coding: How do I make an API?

Show that the API doesn't accept `GET` requests:

    $ http --verbose GET localhost:5000/api/v1/greeting

Show that it detects when we don't give it parameters:

    $ http --verbose POST localhost:5000/api/v1/greeting

Show the API in action:

    $ http --verbose POST localhost:5000/api/v1/greeting name=Radon

## Demo: How do I use an API?

Make an API request in the JavaScript console:

    makeRequest("/api/v1/greeting", { name: "Radon" })

## Demo: How do I use Heroku?

Install the Heroku command-line tools:

    $ brew install heroku/brew/heroku

Create a Heroku application:

    $ heroku create -a cs121-hello-demo

Deploy the application:

    $ git push heroku master

Stream the logs:

    $ heroku logs -t

Install Heroku add-ons:

* Dead Man's Snitch
* Timber.io Logging

Run commands on Heroku's remote machine:

    $ heroku run ...
