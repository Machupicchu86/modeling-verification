# Starter code for "Modeling & Verification" homework #1

## Evaluation

Do **not** fill these tables, do **not** remove them, do **not** touch them,
leave them to your teacher.

Evaluation follows the questions:
* do you have done anything at the deadline?
  (no: 0 points)
  * [ ] Done anything
* do you have understood and implemented all the required notions?
  (yes: 4 points, no: 2 points)
  * [ ] Reachability graph
  * [ ] Coverability graph
  * [ ] Place invariants
  * [ ] Transition invariants
* do you have understood and implemented corners cases of all the required notions?
  (yes: +2 point)
  * [ ] Reachability graph
  * [ ] Coverability graph
  * [ ] Place invariants
  * [ ] Transition invariants
* do you have correctly written and tested your code?
  (no: -0.5 point)
  * [ ] Coding standards
  * [ ] Tests all pass
  * [ ] Code coverage

| Grade |
| ----- |
|       |

## Subject

The goal of this assignment is to check that you have understood several
algorithms on Petri nets, by implementing them:
* reachability graph
  (file `src/reachability_graph.lua`)
* coverability graph
  (file `src/coverability_graph.lua`)
* place invariants
  (file `src/place_invariants.lua`)
* transition invariants
  (file `src/transition_invariants.lua`)

## Environment

* [Moodle](https://moodle.unige.ch)
  Check that you are registered in the "Modeling & Verification" classroom
* [GitHub](https://github.com)
  Create an account if you do not have one already
* Install [VirtualBox](https://www.virtualbox.org)
  We will work in a virtual machine.
* Create a new virtual machine, using [Ubuntu amd64](http://www.ubuntu.com/download/desktop),
  and install `ssh` in it (if needed).
* Run the following scripts to install all required dependencies:

```sh
set -e
curl -L https://github.com/atom/atom/releases/download/v1.10.2/atom-amd64.deb         -o atom-amd64.deb
curl -L https://s3.amazonaws.com/downloads.wercker.com/cli/stable/linux_amd64/wercker -o wercker
sudo -s -- <<"EOF"
  apt-get update
  apt-get install --yes libreadline-dev libssl-dev curl docker.io git python-pip
  usermod -aG docker "${SUDO_USER}"
  pip install hererocks
  dpkg -i atom-amd64.deb
  mv wercker /usr/local/bin/
  chmod a+x /usr/local/bin/wercker
EOF
```

```sh
rm atom-amd64.deb
hererocks --patch --lua=^ --luarocks=^ ${HOME}/.local
luarocks install luasec       OPENSSL_LIBDIR="/usr/lib/x86_64-linux-gnu/"
luarocks install ansicolors
luarocks install argparse
luarocks install busted
luarocks install cluacov
luarocks install luacheck
apm install atom-format-lua
apm install language-lua
apm install linter-luacheck
```

Launch `atom` in the virtual machine, and configure the `linte-luacheck` plugin.
Open the [Command Palette](http://flight-manual.atom.io/getting-started/sections/atom-basics/),
open "View installed packages", and "luacheck" settings.
Configure it by providing the path to `luacheck`.
You can obtain the path by copying exactly the result of command: `which luacheck` (in your terminal).

The environment contains:
* [Git](https://git-scm.com/docs/gittutorial):
  the tool for source code management.
* [Lua](https://www.lua.org):
  the programming language that we will use.
* [Luarocks](https://luarocks.org):
  a package manager for Lua.
* [Wercker](http://wercker.com/cli):
  a tool (and online service) to build and test your source code.
* [Docker](https://www.docker.com):
  a container system, required by `wercker`.
* [Atom](https://atom.io):
  the editor we will use.

## Rules

* If for any reason you have trouble with the deadline,
  please contact your teacher as soon as possible.
* Coding Standards: your source code (and tests) must pass all checks
  **without warnings or errors**.
  Checks are performed using the `luacheck` command.
* Your work will be tested in a dedicated environment,
  using `wercker`.
  You can always run all the tests on your code by running the following
  command, from the root of your project (where the `wercker.yml` file is
  located):

  ```sh
  $ wercker build
  ```
