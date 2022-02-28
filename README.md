# Meme Generator – Instructions
The goal of this project is to build a "meme generator" – a multimedia application to dynamically generate memes, including an image with an overlaid quote.

## Overview

Meme Generator – Instructions
The goal of this project is to build a "meme generator" – a multimedia application to dynamically generate memes, including an image with an overlaid quote. It’s not that simple though! Your content team spent countless hours writing quotes in a variety of filetypes. You could manually copy and paste these quotes into one standard format – but you’re going to over-engineer a solution to load quotes from each file to show off your fancy new Python skills.


### What Will I Build?
You have been called on to demonstrate your newly learned skills to create a dynamic data-rich application to generate images with quotes.


#### The application you build must:

- Interact with a variety of complex filetypes. This emulates the kind of data you’ll encounter in a data engineering role.
- Load quotes from a variety of filetypes (PDF, Word Documents, CSVs, Text files).
- Load, manipulate, and save images.
- Accept dynamic user input through a command-line tool and a web service. This emulates the kind of work you’ll encounter as a full stack developer.
This project will give you a hands-on opportunity to practice what you've learned in this course, such as:

Object-oriented thinking in Python, including abstract classes, class methods, and static methods.
DRY (don’t repeat yourself) principles of class and method design.
Working with modules and packages in Python.
As you're building your project, be sure to demonstrate coding best practices for style and documentation. Ensure your code, docstrings, and comments adhere to [PEP 8 Standards](https://www.python.org/dev/peps/pep-0008/).

You'll find detailed instructions on the following pages. And while you work through the instructions, you can also check your work against the [project rubric](https://docs.google.com/spreadsheets/d/1l0cDsN3T6jfP0TUiTcvqXsLDI-WwpJH44wYatFJLO7o/edit#gid=0) to see exactly what your reviewer will be looking for when they grade your project.

## Starter Code

We've provided some code and data to get you started. So the first step is to download the starter code and get generally familiar with what it includes.

- Download the starter code here.
- Locate the sample quotes and images of Xander the pup in `src/_data/`
- There's a basic flask server that will consume your modules and make them usable through a web interface. Check out the main code for this flask service in `app.py`.
- Check out the HTML template files in `templates/`

## Quote Engine

he Quote Engine module is responsible for ingesting many types of files that contain quotes. For our purposes, a quote contains a body and an author:


```bash
"This is a quote body" - Author
```

This module will be composed of many classes and will demonstrate your understanding of complex inheritance, abstract classes, classmethods, strategy objects and other fundamental programming principles.

### Quote Format
Example quotes are provided in a variety of files. Take a moment to review the file formats in `./_data/SimpleLines` and `./_data/DogQuotes`. Your task is to design a system to extract each quote line-by-line from these files.

### Ingestors
An abstract base class, `IngestorInterface` should define two methods with the following class method signatures:

```bash
def can_ingest(cls, path: str) -> boolean
def parse(cls, path: str) -> List[QuoteModel]
```

Separate strategy objects should realize `IngestorInterface` for each file type (csv, docx, pdf, txt).

TIP: pdftotext may not be installed on your local machine (Mac or Windows). If this is the case, you can install using the open source [XpdfReader utility](https://www.xpdfreader.com/pdftotext-man.html).

A final `Ingestor` class should realize the `IngestorInterface` abstract base class and encapsulate your helper classes. It should implement logic to select the appropriate helper for a given file based on filetype.

NOTE: Do not use the [pdftotext](https://pypi.org/project/pdftotext/) PIP Library - we'd like you to demonstrate your understanding of the subprocess module.

The responsibility of this module is to load and parse quotes from files. Here's what you'll need to do to complete it:

- Create a Python module (including `__init__.py` ) in a directory called `QuoteEngine`.
- Example quotes are provided in a variety of files. Take a moment to review the file formats in `./_data/SimpleLines` and `./_data/DogQuotes`.
- Implement a simple `QuoteModel` class to encapsulate the body and author.
- Implement an abstract base class, `IngestorInterface`. This class should define two methods with the following class method signatures: `def can_ingest(cls, path) -> boolean` and `def parse(cls, path: str) -> List[QuoteModel]`.
- Implement separate strategy objects that realize the `IngestorInterface` for each file type (cv, dox, pdf, txt).
- Implement a final `Ingestor` class that realizes the `IngestorInterface` abstract base class and encapsulates your helper classes. It should implement logic to select the appropriate helper for a given file, based on filetype.
- If you like, you can check your work against the `Quote Engine Module` section of the [rubric](https://docs.google.com/spreadsheets/d/1l0cDsN3T6jfP0TUiTcvqXsLDI-WwpJH44wYatFJLO7o/edit#gid=0).
- All Quote classes have clear, concise, and PEP compliant docstrings.
- All code is PEP-8 Compliant.
- Common exceptions should be handled using try-catch blocks.

## Meme Engine Module

The Meme Engine Module is responsible for manipulating and drawing text onto images. It will reinforce your understanding of object-oriented thinking while demonstrating your skill using a more advanced third party library for image manipulation.

The class must implement code for:

- Loading an image using Pillow (PIL).
- Resizing the image so the width is at most 500px and the height is scaled proportionally.
- Adding a quote body and a quote author to the image.
- Saving the manipulated image.
- The class must implement this instance method signature, which returns the path to the manipulated image: `make_meme(self, img_path, text, author, width=500) > str`.
- You can check your work against the `Meme Generator Module` section of the [rubric](https://docs.google.com/spreadsheets/d/1l0cDsN3T6jfP0TUiTcvqXsLDI-WwpJH44wYatFJLO7o/edit#gid=0).
- All Meme Generator classes have clear, concise, and PEP compliant docstrings.
- All code is PEP-8 Compliant.
- Common exceptions should be handled using `try-catch` blocks.

## Create a README

Now it's time to document your code in order to describe your project's functionality and how to use it!

- Create a `README.md` file in the project root directory.
- The README should include an overview of the project
- The README should include instructions for setting up and running the program
- The README should include a brief description of the roles-and-responsibilities of all sub-modules including dependencies and examples of how to use the module.

## Package your Application

Larger, complex systems need an interface for users to interact with. We'll package the project as a command line tool and as a simple web service.

### Create a Command-Line Interface tool
The project contains a simple cli app starter code in `meme.py`. This file contains `@TODO` tasks for you to complete. The utility can be which can be run from the terminal by invoking `python3 meme.py`

The script must take three optional CLI arguments:

- --body a string quote body
- --author a string quote author
- --path an image path
The script returns a path to a generated image. If any argument is not defined, a random selection is used.

### Complete the Flask app
The project contains a flask app starter code in app.py. This file contains @TODO tasks for you to complete.

The app uses the Quote Engine Module and Meme Generator Modules to generate a random captioned image.

It uses the requests package to fetch an image from a user submitted URL.

The flask server must run with no errors

Make sure you complete the following tasks:

- Open the `meme.py` command line starter code and complete the `@TODOs`.
Open the `app.py` flask web server starter code and complete the `@TODOs`. You can start the server by calling `python3 app.py` from a terminal window
- You can check your work against the Package your Application section of the [rubric](https://docs.google.com/spreadsheets/d/1l0cDsN3T6jfP0TUiTcvqXsLDI-WwpJH44wYatFJLO7o/edit#gid=0).
- Create a requirements. txt file in the project root including all project dependencies.

## Before You Submit

Before you submit your project, take a moment to ensure that it is ready for review:

- You have reviewed each item in the rubric and verified you have completed it successfully.
- The requirements.txt file contains all required dependencies. (TIP: delete your virtual environment and re-instantiate to verify it is complete.)
- You have zipped the project directory and made sure all files are included (so that your reviewer can run your code!).

## Project Submission

You can either submit your project as a link to a GitHub repo or as a zip. Be sure your submission includes all folders and files needed to run your application.

Before submitting, be sure to check out the [rubric](https://docs.google.com/spreadsheets/d/1l0cDsN3T6jfP0TUiTcvqXsLDI-WwpJH44wYatFJLO7o/edit#gid=0) to confirm that your project meets all the required specs.
