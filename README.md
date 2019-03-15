# python_structure

This repo documents my (evolving) ideas about "good" project structure in Python and 
other coding techniques useful in many projects.  

* Tests should be in `tests/` and source should be in `src`.  This allows us to separate
production code from test code, but it also causes problems with `import` statements 
and paths.  We place our code in a package and install it as editable to address the
`import` problem.  To solve the path problems, see the code in `config.py` and its
usage of `__file__`.

* Secrets (API keys, passwords, etc.) should be protected.  This is handled
via `python-dotenv`, which loads values from the `.env` file as environment variables.

## Developer Setup

1. Create a virtual environment

    `python3 -m venv .venv`

2. Activate the virtual environment

    `source .venv/bin/activate`
    
3. Install required libraries

    `pip install -r requirements.txt`
    
4. Install source as an editable package

    `pip install -e .`
    
5. Create the file `.env` containing our sensitive data (that should never go in the repo)

    `secret=42`
    
Once you have completed these steps you should be able to:

* Run `pytest` from the room of the project
* Run `pytest` from `tests/`
* Run `main.py` from anywhere (e.g. `python src/python_structure/main.py`)

## Files and Directories

* `requirements.txt` - The list of required libraries.  
* `setup.py` - The script the `pip` runs to install the package.  The current version is bare-bones.  Many
   other options should be set for a production system.
* `src/python_structure/__init__.py` - Establishes the `python_structure` directory as a package. This file is empty 
   by default.

 
 ## Background Reading
 
 * [An argument](https://hynek.me/articles/testing-packaging/) to use the `src` folder.  This article also
   talks about using `tox`, which is not used in this repo.
*  [In-depth discussion of packaging](https://blog.ionelmc.ro/2014/05/25/python-packaging/), also using a
   `src` directory.  Only the section, "The structure" is relevant to this repo.  The rest goes further into
   configuring testing and continuous integration via TravisCI.
