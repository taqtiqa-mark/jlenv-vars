# jlenv-vars: Set environment variables before spawning Julia processes

This is a plugin for [jlenv](https://github.com/jlenv/jlenv)
that lets you set global and project-specific environment variables
before spawning Julia processes.

## Installation

Make sure you have the latest version of jlenv, then run:

    git clone https://github.com/jlenv/jlenv-vars.git $(jlenv root)/plugins/jlenv-vars

## Precedence

Use `jlenv vars` command to print all environment variables in the
order they'll be set.

1. `~/.jlenv/vars`
1. `.jlenv-vars` from parent folders
1. `.jlenv-vars` from current folder

## Usage

```bash
jlenv help vars
```

Julia [environment variables are documented](https://docs.julialang.org/en/v1/manual/environment-variables/index.html).

Define environment variables in an `.jlenv-vars` file in your project,
one variable per line, in the format `VAR=value`. 
For example:

```bash
JULIA_NUM_THREADS=2
JULIA_ERROR_COLOR="\033[91m"
JULIA_DEPOT_PATH="foo/bar"
```

You can perform variable substitution with the traditional `$`
syntax. For example, to append to `GEM_PATH`:

```bash
JULIA_LOAD_PATH=$JULIA_LOAD_PATH:/u/shared/gems
```

You may also have conditional variable assignments, such that a
variable will **only** be set if it is not already defined or is blank:

```bash
JULIA_LLVM_ARGS?=-debug-only=loop-vectorize
```

In the above case, `JULIA_LLVM_ARGS` will only be set if `$JULIA_LLVM_ARGS` is
currently empty (i.e., if `[ -z "$JULIA_LLVM_ARGS" ]` is true).

Spaces are allowed in values; quoting is not necessary. Expansion and
command substitution are not allowed. Lines beginning with `#` or any
lines not in the format VAR=value will be ignored.

Variables specified in the `~/.jlenv/vars` file will be set
first. Then variables specified in `.jlenv-vars` files in any parent
directories of the current directory will be set. Variables from the
`.jlenv-vars` file in the current directory are set last.

Use the `jlenv vars` command to print all environment variables in the
order they'll be set.

## Version History

**1.0.0** (October 13, 2019)

* Initial public release for Julia.

## License

&copy; 2012 Sam Stephenson. Released under the MIT license. See
`LICENSE` for details.
