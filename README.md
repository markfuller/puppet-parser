# Puppet Language Parser

This is a parser for .pp (puppet) or .epp (embedded puppet) files written in [Go](https://golang.org/).

## The parse program
A command line utility named `parse` is provided. It prints errors and
warnings on _stderr_, and returns a non zero exit status on failure. On success,
it produces a representation of the AST on _stdout_.

Usage:
```
parse [-v][-j] <path to pp or epp file>
```
<table border="0">
    <tr>
        <td><b>-v</b></td>
        <td>Validate only, i.e. suppress generation of AST.</td>
    </tr>
    <tr>
        <td><b>-j</b></td>
        <td>JSON output. Outputs a JSON object with <code>issues</code> and <code>ast</code>
            keys. The <code>issues</code> key will only be present when there were issues.
        </td>
    </tr>
</table>

## The parser package

### What it is
The `parser` go-package is a library that can be used by other applications
that wishes to parse puppet and validate code and use the AST. See [parser.go](main/parser.go)
for sample usage of `Parser` and `Validator`.

### What it is not
This is not a evaluator (A.K.A. compiler). An evaluator that acts on the produced AST would be one way
of using the parser package.

## Getting started
#### Install the go runtime
This step is different depending on platform. On a Redhat/Debian system:
```
$ sudo yum install go
```
#### Set up environment
```
$ export GOPATH="$HOME/go"
$ export PATH="$PATH:$GOPATH/bin"
```
#### Clone this repo into its package location
```
$ mkdir -p "$GOPATH/src/github.com/puppetlabs"
$ cd "$GOPATH/src/github.com/puppetlabs"
$ git clone git@github.com:puppetlabs/go-parser.git
```

#### Install the command
The command is now ready to be installed using `go install`. Since this command acts on the
setting of `GOPATH` it doesn't matter what directory you're in when executing it. The binary
will be installed in `$GOPATH/bin` regardless.
```
$ go install github.com/puppetlabs/go-parser/parse
```

#### Use the command
```
$ parse some_manifest.pp
```

## This is work in progress
This project is work in progress. There is no release yet and absolutely no
guarantee that things will not change radically in the near future.

### What's missing
- The current code needs API documentation
- The Validator is far from complete
- A JSON schema is needed to describe the json format for the AST

## Contributing
Please contact the author [Thomas Hallgren](mailto:thomas.hallgren@puppet.com) if you
have ideas or want to use this code.

