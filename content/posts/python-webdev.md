Title: Web Development with Python
Date: 2020 10 17 23:54

## Python Web Development

I'm working on getting Jinja2, Pelican, Bootstrap, SASS, and maybe later Flask
to play nice with one another. Let's see how this goes. I'm going to take 
notes as I go for future reference.

### Notes
#### Static Site Generator
A static site generator is a program which takes templates and posts and 
whatnot and outputs a complete website as a directory.

Pelican is one written in Python. You can install it with pip (it's a package) 
and you can run it with `python -m pelican` or simply `pelican`.

#### 

### Setup
#### Dependencies
I want to use Python as much as possible, and my research indicates that the 
following are the standard:

- [Jinja2](https://palletsprojects.com/p/jinja/) for templating
- [Pelican](https://docs.getpelican.com/en/stable/) for static site generation 
(an alternative to web serving)
    - [Markdown](https://python-markdown.github.io/), if you want to use 
    Markdown with Pelican
- [Flask](https://flask.palletsprojects.com/en/1.1.x/) for web serving (an 
alternative to static site generation)

Pure HTML and CSS aren't professional, we will use:

- [Bootstrap](https://getbootstrap.com/), the standard front-end HTML/JS 
toolkit
- [SASS](https://sass-lang.com/), the standard CSS preprocessor (integrates 
with Bootstrap)

While you need to download a SASS executable, you don't technically need to 
install Bootstrap yourself (which would require [NodeJS](https://nodejs.org/en/))
 unless you want to do some more advanced serving stuff with Flask.

Anyway, this looks like (in your project directory, on Unix):
```
python -m venv venv/
chmod +x venv/bin/activate
./venv/bin/activate

pip install Jinja2
pip install Pelican
pip install Markdown
```
And then either `npm install sass`, or [something else](https://sass-lang.com/install).

#### Running Quickstart
Run:
```
pelican-quickstart
```

This is going to make four files in root `pelicanconf.py`, `publishconf.py`, 
`tasks.py`, and `Makefile`.

`tasks.py` and `Makefile` create the site:

- They do the same thing, you only need one:
    - `tasks.py` runs with the python package [Invoke](http://www.pyinvoke.org/) 
    - The makefile lets you use [make](https://www.gnu.org/software/make/manual/make.html). 
- They work by simply calling Pelican.
    - For example, you could call `make devserver`, or you could do

```
pelican -lr content/ -o output/ -s pelicanconf.py
```

`pelicanconf.py` and `publishconf.py` are configuration files.

- You can make as many of these as you want, these two are just the default 
ones.
- They are only referenced in `Makefile`/`tasks.py`.
    - If you make your own/want to change the names, edit whichever of 
    `Makefile`/`tasks.py` you use.
    - If you run pelican directly (`python -m pelican` or `pelican`), you 
    just give it as a command line argument (`-s`).
- `pelicanconf.py` is the default settings for development.
    - For example, `SITEURL` will be set to `''`, as if you set it to your 
    actual url, e.g. my_irl.github.io, it would look for css files under 
    me_irl.github.io/themes/css/.
- `publishconf.py` is the default settings for deployment. For example:
    - It makes your site with absolute URLs
    - You can add Google Analytics options.

#### Project Structure

Edits I made:

- Deleted `tasks.py`, I'm fine using `make`.
- Changed my github pages branch to `trunk`, it defaults to `main`.
    - `trunk` is obviously a better default branch name than `master`.
    - You can 