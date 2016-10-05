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
* Create a new virtual machine,
  using [Ubuntu amd64](http://www.ubuntu.com/download/desktop).
* Run the following script to install dependencies:

  ```sh
    curl -s https://raw.githubusercontent.com/cui-unige/modeling-verification/master/bin/install | bash /dev/stdin
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
