# incontext

**incontext** ("in this context") is a general-purpose context discovery and activation mechanism.

```
Usage:
    incontext --init
    incontext [COMMAND [ARG...]]

Executes COMMAND with ARGs in an environment modified by a .context file in
this or an ancestor directory.

.context is expected to be an executable that does the work of modifying
the environment and executing its arguments.

If no COMMAND is specified, launch a shell with the modified environment
instead.

Options:

    --init			Create an example .context script in the current directory.
```

I found that the first thing I do when working on a project is

- change to its directory in my terminal,
- maybe activate a virtualenv or rbenv,
- set a bunch of environment variables, including
- modify the `$PATH` to include a bunch of project-specific scripts,
- modify my `$PS1` to remind me that this shell contains all these modifications,
- and several other steps, depending on the project.

`incontext` allows me to stuff all of that into a short script, activate it from anywhere within my project directory structure, or run a single command in that environment without messing up my current environment.

## Theory of operation

A _context_ is the top-level directory of some project along with environment settings specific to that project. You are "within" that context when your current working directory is a subdirectory of that top-level project directory. Unfortunately, merely having your current directory set does not activate the project-specific environment settings.

`incontext --init` sets up an executable called `.context` in the root of that project directory with some helpful examples, where you may record your settings. Then, `incontext` uses `findup` to locate the nearest `.context` and Bernstein chaining to activate it.

Where you would normally run 
```
python manage.py runserver
```
in an activated `virtualenv` to launch a Django development server, you may instead run 
```
incontext python manage.py runserver
```
to run it in its `virtualenv` without activating that virtualenv for your own shell.

When not given a command, `incontext` defaults to launching a sub-shell. So you can apply all the modifcations you need for your project, then discard them all simply by `exit`ing the subshell.


## Examples

### virtualenv, but also rubyenv

`# TODO FIXME add tested examples to README.md`

### a project needs environment settings

`# TODO FIXME add tested examples to README.md`

### deployment targets staging or production?

`# TODO FIXME add tested examples to README.md`

## Dependencies

[datagrok/findup](https://github.com/datagrok/findup): locates a given filename in the nearest ancestor directory.

## Other tools like `incontext`

Several tools exist that perform context discovery and environment modification:

- [kennethreitz/autoenv](https://github.com/kennethreitz/autoenv/) runs automatically.
- [codysoyland/virtualenv-auto-activate.sh](https://gist.github.com/codysoyland/2198913) bash-specific; virtualenv-specific; runs automatically.
- [direnv](https://direnv.net/) runs automatically; supports 4 shells; context file must be bash syntax.

I prefer tools that do not override `cd` or run automatically everywhere. One reason is because my current directory might contain untrusted code or belong to a different user. `kennethreitx/autoenv` and `direnv` have an "authorized" mechanism to guard against that, though. Another reason is that explicit activation allows me to provide arguments, to e.g. target production instead of development for that invocation.

Some tools incur a lot of complexity by supporting the syntax of a limited set of different shells. `incontext` avoids this by modifying the environment and launching a new instance of the user's preferred shell or command. In this way, `incontext` is syntax-agnostic and will work with any shell. Its `.context` files default to bourne shell syntax, but this has no impact on the interactive shell users use. Finally, if desired, the `.context` file may be replaced by an executable written in any language, as long as it arranges to execute its arguments.

Some tools incur complexity by managing the setting and un-setting of environment variables in the user's current shell. Others eschew un-setting and allow environment settings to "leak" into other contexts when the user changes directories. `incontext` mostly avoids these problems by launching a subshell in a modified environment. Once the user exits the subshell, their original environment is restored.

## License: AGPL-3.0+ with additional permissions

This software is copyright 2017 [Michael F. Lamb][] and released under the terms of the [GNU Affero General Public License, version 3][AGPL-3.0+] (or, at your option, any later version.) with a grant of additional permission that allows you to apply any terms you wish to the output file `.context`. For details, see [LICENSE.md](LICENSE.md).

[Michael F. Lamb]: http://datagrok.org
[AGPL-3.0+]: http://www.gnu.org/licenses/agpl.html
