# Modeling & Verification Homework

This repository contains information about the homework for the course
["Modeling & Verification"](https://moodle.unige.ch/course/view.php?id=183)
at [University of Geneva](http://www.unige.ch).

## Environment

Please install the following environment:
* [Moodle](https://moodle.unige.ch)
  Check that you are registered in the "Modeling & Verification" classroom
* [GitHub](https://github.com)
  Create an account if you do not have one already
* Install [VirtualBox](https://www.virtualbox.org)
  We will work in a virtual machine.
* Create a new virtual machine, using [Ubuntu amd64](http://www.ubuntu.com/download/desktop),
  and install `ssh` in it (if needed).
* Run the following script to install dependencies:

```sh
set -e
curl -L https://github.com/atom/atom/releases/download/v1.10.2/atom-amd64.deb         -o atom-amd64.deb
curl -L https://s3.amazonaws.com/downloads.wercker.com/cli/stable/linux_amd64/wercker -o wercker
sudo -s -- <<"EOF"
  apt-get update
  apt-get install --yes libreadline-dev libssl-dev curl docker.io git nodejs python-pip
  usermod -aG docker "${SUDO_USER}"
  pip install --upgrade pip
  pip install hererocks
  dpkg -i atom-amd64.deb
  mv wercker /usr/local/bin/
  chmod a+x /usr/local/bin/wercker
  rm atom-amd64.deb
EOF
```
* Run the following script to install Lua and its environment:
```sh
hererocks --patch --lua=^ --luarocks=^ ${HOME}/.local
luarocks install luasec OPENSSL_LIBDIR="/usr/lib/x86_64-linux-gnu/"
luarocks install ansicolors
luarocks install argparse
luarocks install busted
luarocks install cluacov
luarocks install luacheck
luarocks install lua-cjson
apm install atom-format-lua
apm install language-lua
apm install linter
apm install linter-luacheck
apm install cson
atom & sleep 10
ln -s "/usr/bin/nodejs" \
      "${HOME}/.local/bin/node"
ln -s "${HOME}/.atom/packages/cson/node_modules/cson/bin/cson2json" \
      "${HOME}/.local/bin/cson2json"
ln -s "${HOME}/.atom/packages/cson/node_modules/cson/bin/json2cson" \
      "${HOME}/.local/bin/json2cson"
cson2json "${HOME}/.atom/config.cson" > "${HOME}/.atom/config.json"
lua -e '
  local json = require "cjson"
  local file = io.open (os.getenv "HOME" .. "/.atom/config.json", "r")
  local data = json.decode (file:read "*all")
  file:close ()
  data ["*"] ["linter-luacheck"] = {
    executable = os.getenv "HOME" .. "/.local/bin/luacheck",
    globals    = {
      "--std=lua53+busted"
    },
  }
  file = io.open (os.getenv "HOME" .. "/.atom/config.json", "w")
  file:write (json.encode (data))
  file:close ()
'
json2cson "${HOME}/.atom/config.json" > "${HOME}/.atom/config.cson"
rm "${HOME}/.atom/config.json"
```

The environment you installed contains:
* [Git](https://git-scm.com/docs/gittutorial):
  the tool for source code management;
* [Lua](https://www.lua.org):
  the programming language that we will use;
* [Luarocks](https://luarocks.org):
  a package manager for Lua;
* [Wercker](http://wercker.com/cli):
  a tool (and online service) to build and test your source code;
* [Docker](https://www.docker.com):
  a container system, required by `wercker`;
* [Atom](https://atom.io):
  the editor we will use.

## Rules

* We use [GitHub Classroom](https://classroom.github.com) for the homework.
* If for any reason you have trouble with the deadline,
  contact your teacher as soon as possible.
* Your source code (and tests) must pass all checks of `luacheck`
  without warnings or errors.
* Your tests must cover at least 80% of the source code (excluding test files).
* Your work will be tested in a dedicated environment, using `wercker`.
  You can always run all the tests on your code with the following command,
  from the root of your project (where the `wercker.yml` file is located):

```sh
$ wercker build
```

## Evaluation

Evaluation follows the questions:
* do you have done anything at the deadline?
  (no: 0 points)
  * [ ] Done anything
* do you have understood and implemented all the required notions?
  (yes: 4 points for all, no: 2 points for none)
  * [ ] algorithm #1
  * [ ] algorithm #2
  * [ ] ...
* do you have understood and implemented corners cases of all the required
  notions?
  (yes: +2 point for all)
  * [ ] algorithm #1
  * [ ] algorithm #2
  * [ ] ...
* do you have correctly written and tested your code?
  (no: -0.5 point for each)
  * [ ] Coding standards
  * [ ] Tests
  * [ ] Code coverage

| Grade |
| ----- |
|       |
