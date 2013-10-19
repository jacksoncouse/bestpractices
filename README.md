# Best Practices and Coding Conventions

This is an opinionated set of guidelines for making digital projects.

The contents of this repository are released under a [Creative Commons CC BY 3.0 License](http://creativecommons.org/licenses/by/3.0/deed.en_US) and were adapted from the [Amnesty International Best Practices Guide](https://github.com/AmnestyInternational/bestpractices), which in turn was adapted from the [NPR Apps Best Practices Guide](https://github.com/nprapps/bestpractices).

## Contents

1. Development 
  1. [Environments](#environements)
  1. [Repositories](#readmes)
  5. [Version control](#version-control)
  2. [Sites and Apps](#sites-and-apps)
    3. Static vs. Dynamic
  6. [Ruby](#ruby)
  7. [Python](#python)
1. Front-end
  3. [HTML and CSS](#html-and-css)
  4. [Javascript](#javascript)
1. Back-end
6. [Servers](#servers)
7. [Databases](#databases)
  1. Document Oriented 
  2. Relational
3. Documentation

## Environements

Use [Vagrant](http://www.vagrantup.com/) and [Puppet](http://puppetlabs.com/puppet/puppet-open-source) to create consistent VirtualBoxes.

## Repositories

### READMEs

Every README should include:

1. A quick project overview
1. Information about the directory structure
1. How to get started developing
1. Code promotion workflow
1. Environments
1. Links to where to find more information.

Plus:

* Document steps to setup the project from a blank slate. (Data loading, etc.) This should include paths to files stored in Dropbox when relevant.
* Document any required environment variables. If these are secrets they should also be stored in the team Dropbox.
* Document any cron jobs that must be installed on the servers. In the app-template this just means using the `crontab` file in the project root.
* Document any server dependencies that are not part of our standard stack. This includes documenting how to install them. Whenever feasible this documentation should be in the form of `fab` commands.

## Sites and Apps

### Naming conventions
Naming things (variables, files, classes, etc.) consistently and intuitively is one of the hardest problems in computer science. To make it easier, follow these conventions:

* Always proceed from more general to more specific. For example, ``widget-skinny`` is better than ``skinny-widget``.
* Strive for parallelism. If you have a `begin()` function, then have an `end()` function (not `stop()` or `done()`).
* Group related names with common prefixes, e.g. `search_query` and `search_address`.
* Prefer more specific terms to more vague ones. If it's an address call it `address`, not `location`.
* When a function operates on a variable, their naming should be consistent. If working with `updates` then `process_updates()`, don't `process_changes()`. 
* Maintain naming conventions between iterables and their iterators: `for update in updates`, not `for record in updates`.

| Prefer...| To... |
| --------- | ----- |
| create | insert, add, new |
| update | change, edit |
| delete | remove, purge |
| setup | init |
| make | build |
| wrapper | wrap | 

(Note: sometimes these words don't mean the same thing, but when they do, prefer the former.)


## HTML and CSS

* Element IDs and class names should always be ``lowercase-with-dashes``.
* Multi-part IDs and class names should always proceed from more general to more specific. For example, ``electris-skinny`` is better than ``skinny-electris``.
* Put modals and JST templates in their own files. In the app-template these belong in the `templates` and `jst` directories, respectively. When this isn't feasible, put modals in the page footer first, followed by inline javascript templates.
* Prefer [HAML](http://haml.info/) over ERB for HTML templates
* Prefer [SASS](http://sass-lang.com/) over LESS for CSS templates
* [KSS](http://warpspire.com/kss/) for documenting and generating CSS styleguides


## Javascript

### General

* Use 4-spaces for indentation (because it's easier to be consistent with Python than it is to switch your editor back and forth).
* Javascript variables names should always be ``lowercase_with_underscores``.
* Static variables and configuration parameters should be in ``TITLECASE_WITH_UNDERSCORES``.
* All global variables should be defined at the top of the file.
* All variables should be constrained to the current scope with ``var``.
* Declare only a single variable on one line.
* End all statements with a semicolon.
* Use spaces after opening and before closing braces and brackets in array and object definitions, i.e. ``{ foo: [ 1, 2, 3 ] }`` not ``{foo:[1,2,3]}``.
* Do not use spaces after opening or before closing parentheses, i.e. ``if (foo == true) {`` and not ``if ( foo == true ) {``. 
* When accessing properties of a data structure (such as one retrieved using ``getJSON``) prefer bracket syntax (``data["property"]``) to attribute syntax (``data.property``).
* Very frequent property references should be cached, i.e. ``var array_length = array.length;``.
* Use ``===`` rather than ``==``. ([Why?](http://www.impressivewebs.com/why-use-triple-equals-javascipt/))
* **Use single-quotes for strings.**

### Libraries

For consistency, prefer the following libraries to others that perform the same tasks:

* [jQuery](http://jquery.com/) for DOM manipulation
* [Underscore.js](http://documentcloud.github.com/underscore/) for functional programming (where Underscore and jQuery overlap, i.e. ``each()``, prefer Underscore)
* [Bootstrap](http://twitter.github.com/bootstrap/) for responsiveness
* [Moment.js](http://momentjs.com/) for datetime handling
* [jPlayer](http://jplayer.org/) for audio/video playback

### jQuery-specific

* jQuery references that are used more than once should be cached. Prefix these references with ``$``, i.e. ``var $electris = $("#electris");``.
* Whenever possible constrain jQuery DOM lookups within the scope of a cached element. For example, ``$electris.find(".candidate")`` is preferable to ``$(".candidate")``.
* Always use [on](http://api.jquery.com/on/), never [bind](http://api.jquery.com/bind/), [delegate](http://api.jquery.com/delegate/) or [live](http://api.jquery.com/live/). ``on`` should also be preferred to "verb events", such as [click](http://api.jquery.com/click/).

## Ruby

### Baseline
- [Community](https://github.com/bbatsov/ruby-style-guide/) coding style and best-practices
- [TomDoc](http://tomdoc.org/) for documentation

### Libraries

For consistency, prefer the following libraries to others that perform the same tasks:

- [Ruby Version Manager](https://rvm.io/) for keeping projects organized
- [Bundler](http://bundler.io/) for keeping gems organized and up to date
- [Casien](http://www.caseincms.com/) for content management backends
- [Middleman](http://middlemanapp.com/) for generating static sites 
- [Padrino](http://www.padrinorb.com/) for light web apps **or** [Rails](http://rubyonrails.org/) for heavy web apps
- [Capistrano](http://www.capistranorb.com/) for automation and deployment

## Python

### Baseline

* [PEP8](http://www.python.org/dev/peps/pep-0008/).
* [Django Coding Style](https://docs.djangoproject.com/en/dev/internals/contributing/writing-code/coding-style/).
* **Use single-quotes for strings.**

### Libraries

For consistency, prefer the following libraries to others that perform the same tasks:

* [Fabric](http://docs.fabfile.org/) for project tasks
* [Flask](http://flask.pocoo.org/) for light web apps **or** [Django](https://www.djangoproject.com/) for heavy web apps 
* [boto](https://github.com/boto/boto) for accessing AWS programmatically
* [pytz](http://pytz.sourceforge.net/) for manipulating timezones
* [psycopg2](http://www.initd.org/psycopg/) for accessing Postgres
* [lxml](http://lxml.de/) for XML/DOM manipulation
* [Requests](http://docs.python-requests.org/en/latest/) for working over HTTP

### Specifics

* When testing for nulls, always use ``if foo is None`` rather than ``if !foo`` so ``foo == 0`` does not cause bugs.
* Always initialize and store datetimes in the UTC timezone. Never use naive datetimes for any reason.
* Always use ``with`` when accessing resources that need to be closed.
* Always access blocking resources (files, databases) as little as possible.
* When accessing a dictionary element that may not exist, use ``get()``. For example, ``os.environ.get('DEPLOYMENT_TARGET', None)``.
* Project settings that will be used by both fabric and other code should be isolated in ``app_config.py``. ``fabfile.py`` and Django's ``settings.py`` should import from this file to prevent duplication.
* Imports should be organized into three blocks: stdlib modules, third-party modules and our own modules. Each group should be alphabetized.
* Avoid ``from foo import *``. It is the mindkiller.

## Version control

### Git

* Don't store binary files (comps, databases) in the repository.
* If a binary object needs to be shared then store it in Dropbox or on S3. If it is part of the setup process (e.g. a database backup) then use fabric commands to read and write it.
* **Never, ever store passwords, keys or credentials in any repository.** (Use environment variables instead and [.gitignore](https://help.github.com/articles/ignoring-files) for configuration files.)

### Github

Use [Github Flow](http://scottchacon.com/2011/08/31/github-flow.html): 

1. Anything in the master branch is deployable
1. To work on something new, create a descriptively named branch off of master (ie: new-oauth2-scopes)
1. Commit to that branch locally and regularly push your work to the same named branch on the server
1. When you need feedback or help, or you think the branch is ready for merging, open a pull request
1. After someone else has reviewed and signed off on the feature, you can merge it into master
1. Once it is merged and pushed to ‘master’, you can and should deploy immediately

Github flow [in the browser](https://github.com/blog/1557-github-flow-in-the-browser):

1. Create a branch right from the repository.
1. Create, edit, and delete files, rename them, or move them around.
1. Send a pull request from your branch with your changes to kick off a discussion.
1. Continue making changes on your branch as needed, updating the pull request automatically.
1. Once the branch is ready to go, the pull request can be merged using the big green button.
1. Branches can then be tidied up using the delete buttons in the pull request, or on the branches page.
1. Repeat.


## Servers

* Environment variables belong in `/etc/environment`. This file should be sourced by cron jobs. (This happens automatically when using `cron.sh`.)
* Data for services provided by this system belong in `/srv`.



## Databases

### Naming conventions

#### General

* Tables, columns, variables and view names should always be ``lowercase_with_underscores``.
* Naming order should be ``general_specific`` for instance, ``tweets_canadian``.

#### Tables

* Tables should have `tbl_` prefix.
* Tables should be plurals of contents, for instance `people` not `person`.

#### Views

* Views should not have a prefix.

#### Reports

* Reports should have standard English conventions for capitalisation and spacing.
* Reports should be named ``team, general to specific``, for instance ``Monthly giving campaign code details``

### Queries

* Use 2-spaces for indentation.
* Keywords, clauses, and operators should always be uppercase.
