# Python 3 "Violent Python" Source Code

Source code for the book "Violent Python" by TJ O'Connor. The code has been
 fully converted to Python 3, reformatted to comply with PEP8 standards and 
 refactored to eliminate issues involving the implementation of deprecated
  modules.

*A conversion similar to this one has been made available by myself on the
 source code of the book "Black Hat Python", by Justin Seitz. Check it out
  [here](https://github.com/EONRaider/blackhat-python3) if you haven't done it
   yet.*

## Usage
Simply make a new directory (DIR) for the project, create a new
 virtual environment or `venv` for it (recommended), clone this repository
  using `git clone` and install the requirements using `pip install`.

```
user@host:~/DIR$ git clone https://github.com/EONRaider/violent-python3
user@host:~/DIR$ python3 -m venv venv
user@host:~/DIR$ source venv/bin/activate
(venv) user@host:~/DIR$ pip install -r requirements.txt
```

## Notes

- The directories and files have been named in a way that they can be easily
 related to the content that is presented at each chapter.
- The frequent use of string concatenation by the author has been replaced by
 string interpolation in order to allow greater readability and conform to a
  more modern standard.
- Names of files, variables, functions, classes and methods now conform to
 PEP 8 naming standards.
- The now deprecated `optparse` module has been replaced for `argparse
` throughout the entire source code. All argument parsing is now contained
 under the `__main__` execution scope for each file. All CLI arguments that were
  mandatory for the execution of scripts but were treated as optional in the
   original code are now implemented as positional. A *usage* prompt is now
    available for all scripts that use `argparse` by supplying a -h argument to
     the CLI.
- All occurrences of `PEP 8: E722 do not use bare except` violations have
 been refactored with more specific exception clauses.
- The author has a habit of opening files and leaving them in this state
 instead of calling the `close()` method on the open file object. For this
  reason all instances of file manipulation have been refactored by using
   context managers.
- Though completely inadequate from the
     perspective of best-practices, the use of global variables was left
      untouched in preference to producing heavy deviations from the original
       code's logic.

## Refactoring
- `chapter01/vuln_scanner.py` was structured in such a way that a non-existent file would lead to a `OSError` exception at runtime. For that
 reason the iteration control that calls `check_vulns()` was moved into the
  conditional statement defined in the main function.
- `chapter02/nmap_scan.py` implemented a main function solely for the purpose
 of calling the deprecated `optparse` module, which has been replaced by
  `argparse`. Because of that the main function was removed. An iteration
   control structure that was part of the `optparse` call in the original
    code was implemented in such a way that a new call to nmap was executed
     for each port scanned. The iteration was moved into the `nmap_scan
     ` function in order to prevent wasting cycles.
- `chapter02/ssh_command.py` had its initialization code moved into the
 `__main__` execution scope. The names of variables used in the outer scope
  that used to conflict with the names of parameters of functions were
   changed. The returning prompt information was originally encoded and now
    has been decoded in order to afford better readability.
- `chapter02/ssh_brute.py` imported `pxssh` as a standalone library, but in
 fact it is a module under the `pexpect` library. The bug led to a
  `ModuleNotFoundError` and has been corrected. The code itself as presented in the
   book is littered with indentation errors that make it unusable. Such
    problems have also been corrected. 
- `chapter02/ssh_brutekey.py` required a number of pre-generated keys to work; 
furthermore the book points the reader to acquire such keys in a URL
 that currently returns a 403 response. Because of that a compressed archive
  containing the keys has been added to the `chapter02` subdirectory.
- `chapter02/ssh_botnet.py` had an unused import statement to `optparse` that
 was removed. It looks like it was a fragment from an aborted attempt to
  implement a CLI to this script. Surprisingly it was just left hanging there, 
  even in the printed version of the book. The code that initializes the
   botnet and issues its commands was organized under the `__main__` execution 
   scope for the sake of standardization. The two commands issued to the bots
    have been unified to avoid an unnecessary number of return statements.

## Contributing

As a matter of common sense, first try to discuss the change you wish to make to
this repository via an issue.

1. Ensure the modifications you wish to introduce actually lead to a pull
request. The change of one line or two should be requested through an issue
 instead.
2. If necessary, update the README.md file with details relative to changes to
 the project structure.
3. Make sure the commit messages that include the modifications follow a
 standard. If you don't know how to proceed, [here](https://chris.beams.io/posts/git-commit/)
  is a great reference on how to do it.
4. Your request will be reviewed as soon as possible (usually within 48 hours).

