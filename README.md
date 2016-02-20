cheats
======

`cheats` is a command line utility that allows you to define interactive cheat sheets for the command line.
This is intended mainly for command that you use frequently, but not frequently enough to remember them.

`cheats` was inspired by [`cheat`](https://github.com/chrisallenlane/cheat) by chrisallenlane, although it contains none of its code. There is also a [bash reimplementation of `cheat`](https://github.com/jahendrie/cheat) by jahendrie.

Installation
------------

* Automatic installation: Run `install.sh`.
* Manual installation: Put `cheats.sh` somewhere and source it on bash startup (for example, `echo -en '\n\n' | cat - cheats.sh >> ~/.bashrc`), then copy the cheats folder into your home folder (`cp -r cheats ~/.cheats`).
* To update an existing installation, you can run `install.sh` again or manually update `cheats.sh` and the `.cheats` folder.

Usage
-----

    $ cheats dd
    dd 1
    Backup your primary drive
    dd if=/dev/sda of=$backup
    ------------------------------------------------
    dd 2
    Burn a disc image
    dd if=$file of=/dev/cdrom
    
    $ cheats dd 1
    Backup your primary drive
    dd if=/dev/sda of=$backup
    Backup file path> [prompt]
    [dd runs]

If the argument(s) match(es) exactly one cheat, then that cheat is run.
Otherwise, all matching cheats are printed, and you can select one.

Defining cheats
---------------

Cheats are placed in the ~/.cheats directory, with one file per cheat.
Each cheat has the following format:

    One-line description
    The command itself, where $variables can be defined like $this
    variablename:Prompt
    # comment line
    other_variable:Prompt 2
    ...

Any variables that you declare from the third line on will be prompted from the user and placed into the command where necessary.
(It's completely okay if the variable isn't in the command; this is useful for “Are you sure?“ type prompts where you don't care about the input, but want the user to press enter before taking action.)
Any variables left in the command after the prompts are inserted are replaced by bash, if they are present (things like $PWD, $PS1 etc.).
Comment lines are only allowed in the “prompts” section (beginning with the third line) and must start with a ‘#’ (no preceding whitespace is allowed).

System requirements
-------------------

`cheats` was written for `bash`, and by now it contains so much bash-specific syntax that running it on other shells may require considerable porting efforts. I have tested the following shells:

  * `sh`: Not going to happen. Sorry.
  * `zsh`: Displaying cheats works, running them only works if they don’t contain variables. Completion doesn’t work either. There might be a relatively simple fix for running cheats if you know `zsh` (completion will probably need a rewrite), but I don’t. If you think you can fix it, off to CONTRIBUTING.md with you!
  * `csh`, `ksh`: Doesn't work at all. I also have no knowledge of these shells, so I don't know if it even could work.

Other than your shell, the following commands are used: `printf`, `basename`, `head`, `tail`, `sed`, `tput`. For most package managers, `sed` is in package “sed”, `tput` is in package “ncurses”, and the rest are part of “coreutils”.

License
-------

The content of this repository is released under the MIT License as provided in the LICENSE file that accompanied this code.

By submitting a "pull request" or otherwise contributing to this repository, you agree to license your contribution under the license mentioned above.
