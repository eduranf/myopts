# myopts

[![NPM version][npm-image]][npm-url]
[![js-standard-style][standard-image]][standard-url]

> convert python docstrings with options into markdown

This module provides a command line tool for parsing a Python file and generating nice looking markdown with your function definitions. It's extremely opinionated and rigid! But also extremely easy to use. 

I wrote it because [Sphinx](http://www.sphinx-doc.org/en/stable/), the main documentation framework for Python, is complicated, involves a lot of configuration, and exports to re-structured text. Especially for small projects, I want to write documentation in markdown and just combine it with automatically generated function and option signatures. This module helps you do that!

Why `myopts`? There's a bug called [*`Paonias myops`*](http://bugguide.net/node/view/3713/bgimage) that's also known as the small-eyed Sphinx.

## install

Install the command line tool as

```
npm install myopts -g
```

## example

Put this into a file `function.py`

```python
def coolfunction(parameter, option=1000):
    """
    This is a docstring.

    Parameters
    ----------
    option : int, optional, default = 10
        Description of the option.
    """
```

And then call `myopts function.py` to get the following markdown

```markdown
#### `coolfunction(parameter, option=1000)`

This is a docstring.

- **`option`** `int` `optional` `default = 10`

   Description of the option.
```

Which renders as

#### `coolfunction(parameter, option=1000)`

This is a docstring.

- **`option`** `int` `optional` `default = 10`

   Description of the option.

## usage

Just specify a python file, and any associated options. Markdown will be sent to stdout, or written to a file.

```
myopts <source> -o <output> -c <classname> -t <title> -s <sort>
```

The options are:

- `output` whether to write to an output file
- `classname` if specified, will document all methods for this class
- `title` if specified, will add a heading to the top with the given title
- `sort` if true, will sort functions by name 

## format

The parsing in `myopts` only works on a rigid set of docstring formats, more or less the "numpydocs" style.

You can provide a Python module with one or more functions in the form

```python
def coolfunction(parameter, option=1000):
    """
    This is a docstring.

    Parameters
    ----------
    option : int, optional, default = 10
        Description of the option.

    another : int, optional, default = 200
        Description of another option.
    """
```

Or you can provide a class with one or more class methods

```python
class CoolClass:
    def coolfunction(self, parameter, option=1000):
        """
        This is a docstring.

        Parameters
        ----------
        option : int, optional, default = 10
            Description of the option.

        another : int, optional, default = 200
            Description of another option.
        """
```

In either case, the following conventions are assumed:
- all docstrings are demarcated above and below with `"""`
- all parameters are listed under the `Parameters` heading
- there is a `:` between a parameter name and its annotation
- parameter annotations are comma-separated
- each parameter has a one or many line description followed by a line break 

If you write your docstrings any differently, `myopts` probably won't work! 

## contributing

A couple simple features that'd be good to add
- Support for other headings like `Returns` and `Example`
- Throw errors if formatting deviates from expectation, rather than produce garbage

If you want to add one of these, or if you find the intended behavior doesn't work, issues and PRs welcome!

## license

[MIT](LICENSE)

[npm-image]: https://img.shields.io/badge/npm-v1.0.0-lightgray.svg?style=flat-square
[npm-url]: https://npmjs.org/package/myopts
[standard-image]: https://img.shields.io/badge/code%20style-standard-lightgray.svg?style=flat-square
[standard-url]: https://github.com/feross/standard

