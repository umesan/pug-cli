# pug-cli

Pug's CLI interface

[![Build Status](https://img.shields.io/travis/pugjs/pug-cli/master.svg)](https://travis-ci.org/pugjs/pug-cli)
[![Dependency Status](https://img.shields.io/david/pugjs/pug-cli.svg)](https://david-dm.org/pugjs/pug-cli)
[![NPM version](https://img.shields.io/npm/v/pug-cli.svg)](https://www.npmjs.org/package/pug-cli)
[![Coverage Status](https://img.shields.io/codecov/c/github/pugjs/pug-cli.svg)](https://codecov.io/gh/pugjs/pug-cli)

## Edit
下記の理由により、pug-cliを forkしてカスタマイズ。

- 現在、[npm](https://www.npmjs.com/package/pug-cli)からインストールできる、[pug-cli 1.0.0-alpha6](https://www.npmjs.com/package/pug-cli)は、  
パーシャル指定（ファイル先頭に_をつける）に対応していない。
- [puc-cli/master](https://github.com/pugjs/pug-cli/tree/master)は対応済みだが、npmに反映していない模様

- ファイルの先頭に _をつけた.pugファイルのみを除外したい。  
`npm-cli/master`はディレクトリ名の先頭に_が入っている場合、  
ディレクトリ内の.pugをコンパイル対象外にするようになっている。

>[参考サイト]  
>https://qiita.com/soarflat/items/48cec8fb19252a3fc4ad
>https://qiita.com/TakashiShibusawa/items/2e15ab05d61c3f8fd33a


## Usage

```
$ pug [options] [dir|file ...]
```

Render `<file>`s and all files in `<dir>`s. If no files are specified,
input is taken from standard input and output to standard output.

### Options

```
-h, --help             output usage information
-V, --version          output the version number
-O, --obj <str|path>   JSON/JavaScript options object or file
-o, --out <dir>        output the rendered HTML or compiled JavaScript to
                       <dir>
-p, --path <path>      filename used to resolve includes
-b, --basedir          path used as root directory to resolve absolute includes
-P, --pretty           compile pretty HTML output
-c, --client           compile function for client-side runtime.js
-n, --name <str>       the name of the compiled template (requires --client)
-D, --no-debug         compile without debugging (smaller functions)
-w, --watch            watch files for changes and automatically re-render
-E, --extension <ext>  specify the output file extension
-s, --silent           do not output logs
--name-after-file      name the template after the last section of the file
                       path (requires --client and overriden by --name)
--doctype <str>        specify the doctype on the command line (useful if it
                       is not specified by the template)
```

### Examples

Render all files in the `templates` directory:

```
$ pug templates
```

Create `{foo,bar}.html`:

```
$ pug {foo,bar}.pug
```

Using `pug` over standard input and output streams:

```
$ pug < my.pug > my.html
$ echo "h1 Pug!" | pug
```

Render all files in `foo` and `bar` directories to `/tmp`:

```
$ pug foo bar --out /tmp
```

Specify options through a string:

```
$ pug -O '{"doctype": "html"}' foo.pug
# or, using JavaScript instead of JSON
$ pug -O "{doctype: 'html'}" foo.pug
```

Specify options through a file:

```
$ echo "exports.doctype = 'html';" > options.js
$ pug -O options.js foo.pug
# or, JSON works too
$ echo '{"doctype": "html"}' > options.json
$ pug -O options.json foo.pug
```

## Installation

    npm install pug-cli -g

## License

MIT
