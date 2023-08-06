<p align="center">
	<br/>
    <img src="https://user-images.githubusercontent.com/1223459/87218719-d185e300-c31a-11ea-897b-0db31b956ff1.png"  width="700px">
	<br/>
	<br/>	
</p>



[![license: Apache 2.0](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](https://shields.io/)
[![version: 0.10.0](https://img.shields.io/badge/version-0.9.3-default.svg)](https://shields.io/)
[![platforms: macos,linux,windows](https://img.shields.io/badge/platforms-macos%20|%20linux%20|%20windows-orange.svg)](https://shields.io/)
[![goreportcard](https://goreportcard.com/badge/github.com/vakenbolt/go-test-report)](https://goreportcard.com/report/github.com/vakenbolt/go-test-report)

`go-test-report` captures `go test` output and parses it into a _single_ self-contained HTML file. 

## Installation

Install the go binary using `go get`.

> **NOTE:** To run the binary, add the `bin` folder from go's workspace directory to the exported `PATH` variable in your shell. The default workspace folder is a directory named go within your user home directory (`~/go` for Linux and macOS, `%USERPROFILE%/go` for Windows).


```shell
$ go get -u github.com/jdsmdev/go-test-report/
```

## Usage

To use `go-test-report` with the default settings. 

```shell script
$ go test -json | go-test-report
```

The aforementioned command outputs an HTML file in the same location. 

```shell
test_report.html
```

>Everything needed to display the HTML file correctly is located inside of the file, providing an easy way to store and host the test results.

#### Understanding HTML test report

The HTML file generated by `go-test-report` is designed to provide an easy way to navigate test results. At the top of the page are general stats related to the test. Below is the title of the test followed by a section called _"Test Groups"_. Tests are organized into these groups which are represented by color-coded squares. A <span style="color: green">green</span> square indicates that all test in that group passed. 

<p align="center">
	<br/>
	<img src="https://user-images.githubusercontent.com/1223459/116140607-3093c900-a69d-11eb-9f03-f5d43f224dbf.png" width="700px" style="border: 1px #cccccc solid; padding: 8px">
	<br/>
	<br/>	
</p>

A <span style="color: red">red</span> square indicates that at least one test in that group failed.  

<p align="center">
	<br/>
	<img src="https://user-images.githubusercontent.com/1223459/87218926-c9c73e00-c31c-11ea-9834-057d92de98bd.png" width="216px" style="border: 1px #cccccc solid; padding: 8px">
	<br/>
	<br/>	
</p>

To view the tests in a particular test group, click on any of the test group indicators. A selected group indicator will be colored in black. The number of tests allocated per test group can be set with the `groupSize` command-line flag.

<p align="center">
	<br/>
	<img src="https://user-images.githubusercontent.com/1223459/116140445-f5919580-a69c-11eb-922e-78e6b8487f67.png" width="700px" style="border: 1px #cccccc solid; padding: 8px">
	<br/>
	<br/>	
</p>

To view the output of a related test, click on the title of a test on the list. If you want to expand _all_ of the test on the list, simultaneously press `shift` and the test group indicator.

<p align="center">
	<br/>
	<img src="https://user-images.githubusercontent.com/1223459/87218282-d9438880-c316-11ea-9a81-54d4cd5b6d85.png" width="700px" style="border: 1px #cccccc solid; padding: 8px">
</p>


## Configuration
Additional configuration options are available via command-line flags.

```
Usage:
  go-test-report [flags]
  go-test-report [command]

Available Commands:
  help        Help about any command
  version     Prints the version number of go-test-report

Flags:
  -g, --groupSize int   the number of tests per test group indicator (default 20)
  -h, --help            help for go-test-report
  -o, --output string   the HTML output file (default "test_report.html")
  -s, --size string     the size (in pixels) of the clickable indicator for test result groups (default "24")
  -t, --title string    the title text shown in the test report (default "go-test-report")
  -v, --verbose         while processing, show the complete output from go test

Use "go-test-report [command] --help" for more information about a command.
```

The name of the default output file can be changed by using the `-o` or `--output` flag. For example, the following command will change the output to _my-test-report.html_.

```bash
$ go test -json | go-test-report -o my-test-report.html
```


To change the default title shown in the `test_report.html` file.

```bash
$ go test -json | go-test-report -t "My Test Report"
```


The default number of tests in a _test group_ can be changed using the `-g` or `--groupSize` flag. For example, the following command will change the default number of tests in a group to 8.

```bash
$ go test -json | go-test-report -g 8
```



Use the `-s` or `--size` flag to change the default size of the _group size indicator_. For example, the following command will set both the width and height of the size of the indicator to 48 pixels. 

```bash
$ go test -json | go-test-report -s 48
``` 

Additionally, _both_ the width and height of the _group size indicator_ can be set. For example, the following command will set the size of the indicator to a width of 32 pixels and a height of 16 pixels.

```bash
$ go test -json | go-test-report -g 32x16
```

## Building from source

[GNU make](https://www.gnu.org/software/make/) is used as the main build automation tool for go-test-report. MacOS users may need to upgrade their local `make` to the latest version using [homebrew](https://brew.sh/).

```bash
$ brew install homebrew/core/make
```

> After the update is complete `make` will become `gmake`

To build `go-test-report` from source.

```bash
$ gmake genbuild
```

Because `go-test-report` embeds the HTML and Javascript code necessary to generate the report output file, a command to generate the embedded go code is needed. 

```bash
$ gmake gencode
```
> Alternatively, `make genbuild` can be used which automatically runs `gencode` _before_ `genbuild`


To build the testing container _(This is the same docker image used during build automation)_:

```bash
$gmake dockertest
```

To build release binaries,

```bash
$ gmake buildall
```
> Creates a folder in the root project folder called `release_builds` that contains builds for the following platforms:
> 
> - `darwin/amd64` (MacOS)
> - `linux/amd64`
> - `windows/amd64`

## Contributors

[@afbjorklund](https://github.com/afbjorklund)
[@quarckster](https://github.com/quarckster)
[@vakenbolt](https://github.com/vakenbolt)


## Contribute & Support

- Add a GitHub Star
- Suggest [new features, ideas and optimizations](https://github.com/vakenbolt/go-test-report/issues)
- [Report issues](https://github.com/vakenbolt/go-test-report/issues)
