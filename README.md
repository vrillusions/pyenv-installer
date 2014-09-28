# pyenv installer

This tools is used to install `pyenv` and friends.

This plugin was inspired from [rbenv-installer](https://github.com/fesplugas/rbenv-installer).

## Existing installations

If you already have `virtualenvwrapper` you will need to remove it and all the various things in your profile so it doesn't load. There's a couple ways of doing the install (ex `virtualenv-burrito`) so check where you got it for uninstall instructions.

## Installation

Install [pyenv](https://github.com/yyuu/pyenv) and friends by running:

    $ wget https://raw.githubusercontent.com/vrillusions/pyenv-installer/master/etc/initial-env
    # Edit initial-env to your liking
    $ source ./initial-env
    $ curl -L https://raw.githubusercontent.com/vrillusions/pyenv-installer/master/bin/pyenv-installer | bash

See the file for a list of all environment variables that can be set

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
