# jcr - compile, run and test Java programs

`jcr` is an almost feature complete replacement for FRI's `tj.exe` for Linux,
which eases the process of compiling, running and testing simple Java programs.

## Installation

The easiest way to use jcr is to simply download the script
and make it executable:

`wget https://git.sr.ht/~erazemkokot/jcr/blob/master/jcr && chmod +x jcr`

This will pull the latest jcr release from [Sourcehut](https://sourcehut.org/).

Of course you can just use the wget command by itself and make the file
executable in a file manager.

**The above command will download jcr to your current directory,
so you will have to prepend every command with a `./`
(e.g. `./jcr Test.java`)**

### Making the script runnable from anywhere

If you want to work with multiple folders,
you might want to add jcr to your PATH.

To do this first make a `bin` folder in your home directory:

`mkdir ~/bin` (the `~` denotes your home directory)

then download the file to the bin directory as before,
but this time specify an output file argument as well:

`wget https://git.sr.ht/~erazemkokot/jcr/blob/master/jcr -o ~/bin/jcr`

finally you can make the script executable:

`chmod +x ~/bin/jcr`

Or in a single command:

`mkdir ~/bin && wget https://git.sr.ht/~erazemkokot/jcr/blob/master/jcr
-o ~/bin/jcr && chmod+x ~/bin/jcr`

This way you can be in any folder and normally execute jcr
(e.g. `jcr Test.java`)

## Features

`jcr` is almost fully backwards compatible with `tj.exe`,
excluding the html file generation (do we really need that anyway?).

Its features include:

* Compiling and running Java programs with a single command
* Easily adding as many (Scanner) inputs as you want
(instead of echoing them to the program)
* Testing Java programs with premade inputs and outputs from a folder
* Running only some of the tests that are available (`tj.exe`'s -p flag)
* Time limiting individual tests (kill the test if it has not finished)
* Showing Java error messages of failed tests
* Showing the amount of time it took to execute each test
* Automatically removing all Java .class files

### Differences between jcr and tj.exe

Although `jcr` tries to be as backwards compatible with `tj.exe` as possible,
there are some diferences, most notably:

* `jcr` doesn't and never will generate an HTML result of the tests
(it does optionally show Java error messages though)
* `jcr` allows compiling and running Java programs with optional arguments
in a single command, while `tj.exe` doesn't
(although to be fair, `tj.exe` wasn't designed for this)

## Usage

This section will shortly describe what each `jcr` argument does and how
to use them.
You can find the same info by running `jcr -h`.

Usage: `jcr (OPTIONS) [FILE]`

The file must be a Java file with a `.java` extension (e.g. File.java).

Most options can be combined with others to increase functionality.
Examples of this are shown below.

### Options

* `-h` or `--help`

Shows the help menu, listing all the commands that `jcr` uses and its syntax.

* `-v` or `--version`

Shows the version number and copyright info.

* `-t` or `--time`

Enables a time counter, which shows how long each test took.

* `-l` or `--limit`

Enables limiting the time a test can take before being killed.
If a test is killed it shows up as failed.

The command requres one number as an argument - the number of seconds to wait
before killing a test.

* `-p` or `--partial`

Enables advanced test selection.
By default `jcr` tests all the inputs/outputs it finds
in the provided directory.
With this option enabled you may select only a few tests to run (or just one).

The command requires one argument, either a single number to select
a specific test to run, multiple numbers separated with commas (eg. 1,2,3),
or two numbers with a dash in-between (e.g. 8-10),
to run the tests between the two numbers (inclusively).
The example above would run tests 8, 9 and 10.

If you select a test number that is higher than the files that were found
in the provided directory, jcr will warn you and only
execute the tests available.

* `-e` or `--errors`

jcr by default only tells you if a test has succeded or failed and does
not show which errors have occured.

This command makes jcr output any Java error messages,
which can help debug code.

It, however, will not tell you what was wrong with your input if there
weren't any Java compilation/runtime errors.

### Examples

Here are some example usages of jcr:

```
jcr File.java                       (compiles and runs the program)
jcr File.java tests/                (tests the program with all files found in the directory "tests")
jcr -e File.java tests/             (same as before but shows Java error messages)
jcr -t File.java tests/             (also shows how long each test took)
jcr -p 4-7 File.java tests/         (only runs tests 4, 5, 6 and 7)
jcr -l 10 File.java tests/          (limits each test to 10 seconds)
jcr -e -t File.java tests/          (shows Java error messages and the time each test took)
```

## Contributing

To help improve `jcr` you can send a patch to `(contact [at] erazem [dot] eu)`,
along with a description of the contribution and optionally your name for
attribution.

I'm also happy to accept feature requests and bug reports sent to my email
or submitted on the [bug tracker](https://todo.sr.ht/~erazemkokot/jcr).

## License

Licensed under the [GNU Affero General Public License](LICENSE).
