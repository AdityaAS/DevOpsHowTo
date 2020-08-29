## Prerequisites
- `pip install recommonmark`
- `pip install rtcat-sphinx-theme`
- `pip install sphinx-server`
- `pip install sphinxcontrib-apidoc`
- `pip install sphinxcontrib-napoleon`


## Setting up Sphynx for a project (Required only once at the beginning)
- Clone the repo `git clone git@github.com:AdityaAS/<name_of_repo_to_add_sphinx>`
- Change directory `cd <name_of_repo_to_add_sphinx>`
- Create a docs directory and `cd` into it i.e. `mkdir docs; cd docs`
- Enter `sphynx-quickstart` to create a barebones doc page with  main title, author name and version number
- Replace conf.py with conf.py from this folder (`./conf.py`)

## How to display python doc strings on Sphinx web page
- Make sure all necessary functions have docstrings in google format (https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html)
- Run the command `sphinx-apidoc -o ./api ../ ../tests/`  -  This will parse all the python files and create appropriate html files
- Execute sphynx by `sphinx-build -W -b html . _build/html/` or `make html` to generate the entire documentation website

## Add additional documentation pages (Introduction, Getting Started etc.)
- Create a markdown file with name (say introduction.md)
- Add a line introduction in `index.rst` so that a hyperlink appears on the main page.
- If hyperlink is needed on a different page (say you want to nest another page inside introduction, add name of markdown introduction_nest inside introduction.md )

## Hosting Sphinx
- Go to the `_build/html` directory and run `python -m http.server` to host the website
- Access documentation via `localhost:8000` or `<ip_of_server>:8000`

