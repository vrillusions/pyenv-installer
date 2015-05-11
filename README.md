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
    $ bash <(curl -fsSL https://raw.githubusercontent.com/vrillusions/pyenv-installer/master/bin/pyenv-installer)

See the file for a list of all environment variables that can be set. That final line is just a shortcut for calling curl and then run the script afterwards.

## OS X setup

On OS X it's better to just use [homebrew](http://brew.sh).  Once homebrew is up and running then run the following to install everything

    brew install readline pyenv pyenv-pip-rehash pyenv-virtualenv pyenv-which-ext
    # This next line is optional but speeds up compiling
    brew install ccache pyenv-ccache

Then add the following to your `~/.bash_profile` to setup pip and vritualenv. I try to move configs to `~/.local/share` and `~/.config` when I can but the default `PYENV_ROOT` is `~/.pyenv` if you want to change it.

    export PYENV_ROOT="${HOME}/.local/share/pyenv"
    export PATH="${PYENV_ROOT}/bin:${PATH}"
    if command -v pyenv 1>/dev/null; then
        # virtualenv modifies the PROMPT_COMMAND by placing it's command in front of
        # what was previously there. This swaps it so previous prompt command is
        # first and then virtualenv's. If this causes problems for you then remove
        # the lines before and after the evals
        #
        # Skip this if we already loaded it
        if [[ ${PYENV_INIT:-0} -eq 0 ]]; then
            _previous_prompt_command="${PROMPT_COMMAND:+${PROMPT_COMMAND};}"
            unset PROMPT_COMMAND
            eval "$(pyenv init -)"
            eval "$(pyenv virtualenv-init -)"
            export PROMPT_COMMAND="${_previous_prompt_command}${PROMPT_COMMAND%;*}"
            unset _previous_prompt_command
            export PYENV_INIT=1
        fi
    fi

    # In Yosemite you need to set the CFLAGS so it includes a couple extra
    # locations. If you run in to issues compiling other software than try
    # commenting out these lines. While this directly related to pyenv these options
    # may be helpful even when not using pyenv
    # Xcode
    CFLAGS="-I$(xcrun --show-sdk-path)/usr/include"
    # Homebrew installed readline
    CFLAGS="-I/usr/local/opt/readline/include ${CFLAGS}"
    # Other homebrew installed libraries
    CFLAGS="${CFLAGS} -I/usr/local/include"
    # Supposed to be LD_LIBRARY_PATH but seems this is the var in os x
    [ -n "${LIBRARY_PATH}" ] && LIBRARY_PATH="${LIBRARY_PATH}:/usr/local/lib" \
        || LIBRARY_PATH="/usr/local/lib"
    export CFLAGS
    export LIBRARY_PATH

Then setup your initial version like so.  A good default version is the same that came with your system.  Run `python -V` to see the current version. You'll need to relogin or run the above options manually so you can use `pyenv`.

    pyenv install --list
    # choose the version you want
    # Important: make sure CFLAGS is set from above or you'll get compile errors
    pyenv install 2.7.8
    pyenv global 2.7.8
    pyenv version

That final command should show your current version of python is 2.7.8 and coming from pyenv.

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

* Install dependencies in Ubuntu and RedHat family (tested with CentOS 6). Can be disabled with `export PYENV_SKIP_UPDATE=true`.
* Switch git clone urls back to https for extra security
* Couple places in output recommend `XDG_DATA_HOME` directory of `$HOME/.local/share` for data storage
* Can install a version of python, which is needed for `virtualenvwrapper` (bash only)
* Include instructions on how to setup on OS X

#### 20130601

 * Initial public release.

### License

(The MIT License)

* Copyright (c) 2013-2014 Yamashita, Yuu and Contributors

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
