# pyenv installer

This tools is used to install `pyenv` and friends.

This plugin was inspired from [rbenv-installer](https://github.com/fesplugas/rbenv-installer).

## Existing installations

If you already have `virtualenv` or `virtualenvwrapper` you will need to remove it and all the various things in your profile so it doesn't load. There's a couple ways of doing the install (ex `virtualenv-burrito`) so check where you got it for uninstall instructions.

## Installation

Install [pyenv](https://github.com/yyuu/pyenv) and friends by running:

    $ curl -L -O https://raw.githubusercontent.com/vrillusions/pyenv-installer/master/etc/initial-env
    # Edit initial-env to your liking
    $ source ./initial-env
    $ curl -s -L https://raw.githubusercontent.com/vrillusions/pyenv-installer/master/bin/pyenv-installer | bash

See the file for a list of all environment variables that can be set. Also there is currently a bug, #2, where if you have the installer setup packages in ubuntu it won't continue the script afterwards. Current workaround is running the second curl command again.

## Workflow

If used to `virtualenvwrapper` then the workflow changes a bit. What used to be this with `virtualenvwrapper`

    mkvirtualenv SpiffyEnv
    cd ~/code/SpiffyEnv
    workon SpiffyEnv

Becomes:

    pyenv virtualenv SpiffyEnv
    cd ~/code/SpiffyEnv
    pyenv local SpiffyEnv

If not using the current active version, then you can set a version with `pyenv virtualenv 3.4 SpiffyEnv`.

Note that the concept of project directories doesn't exist in `pyenv` so you can't have `workon` automatically go to the project directory. Calling `pyenv local SpiffyEnv` above creates a file in current directory called `.python-version` with the content `SpiffyEnv`. Now whenever you `cd` to that folder it will automatically update the `SpiffyEnv` environment for you. `pyenv` considers an actual version and a virtualenv version as the same as far as `pyenv versions` is concerned.

What do when running a pyenv virtualenv from cron is yet to be explored

## Updating

To update pyenv and friends by running:

    $ pyenv update

## Uninstallation

Everything of `pyenv` are installed within `$PYENV_ROOT` (default: `~/.pyenv`). To uninstall, just removing it.

    $ rm -fr ~/.pyenv

## Version History

#### forked from upstream, no version yet

* Use `virtualenvwrapper` instead of `virtualenv`
* Install dependencies in Ubuntu. Can be disabled with `export PYENV_SKIP_UPDATE=true`.
* Switch git clone urls back to https for extra security
* Couple places in output recommend `XDG_DATA_HOME` directory of `$HOME/.local/share` for data storage
* Can install a version of python, which is needed for `virtualenvwrapper` (bash only)

#### 20130601

 * Initial public release.

### License

(The MIT License)

* Copyright (c) 2013 Yamashita, Yuu

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
