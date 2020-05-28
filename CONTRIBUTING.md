# Contributing

First off, thanks for considering to contribute to the FreeProving project!
Whether it is a feature request, enhancement proposal, bug report or pull request, all kinds of contributions are welcome and greatly appreciated.

We want to make the process of contributing to this project as easy and transparent as possible.
Thus, please take the time to read this document carefully if this is your first time contributing.
Note that the following is a set of guidelines and recommendations.
They are not rules and they are certainly not complete.
If you have questions or want to propose changes to this document, feel free to open an [issue][guidelines/issues] or [pull request][guidelines/pull-requests].

## Table of Contents

 1. [Code of Conduct](#code-of-conduct)
 2. [What Should I Know Before I Get Started?](#what-should-i-know-before-i-get-started)
 3. [How Can I Contribute?](#how-can-i-contribute)
    1. [Reporting Bugs](#reporting-bugs)
    2. [Suggesting Enhancements](#suggesting-enhancements)
    3. [Contributing Code](#contributing-code)
 4. [Additional Software](#additional-software)
 5. [Directory Structure](#directory-structure)
 6. [Testing](#testing)
    1. [Running Unit Tests](#running-unit-tests)
    2. [Writing Unit Tests](#writing-unit-tests)
    3. [The CI Pipeline](#the-ci-pipeline)
    4. [Running The Pipeline Locally](#running-the-pipeline-locally)
 7. [Styleguides](#styleguides)
    1. [Languages without Styleguide](#languages-without-styleguide)
    2. [General Guidelines](#general-guidelines)
    3. [Git Commit Messages](#git-commit-messages)
    4. [Haskell Styleguide](#haskell-styleguide)
    5. [Haddock Styleguide](#haddock-styleguide)
    6. [Markdown Styleguide](#markdown-styleguide)
 8. [Legal Information](#leagal-information)
    1. [Privacy](#privacy)
    2. [License](#license)

## Code of Conduct

The Free Proving project and everyone participating in it is governed by our [Code of Conduct][guidelines/CODE_OF_CONDUCT].
By participating, you are expected to uphold this code.
Please report unacceptable behavior to the project maintainers responsible for enforcement at [sad@informatik.uni-kiel.de](mailto:sad@informatik.uni-kiel.de).

## What Should I Know Before I Get Started?

The FreeProving project is made up of [multiple repositories][GitHub] which share these common contribution guidelines.
Before contributing to the FreeProving project, you have to know which repository you actually what to contribute to.
The following is a list of the most important repositories and an explanation of their role in the FreeProving project.

 - The [free-compiler][] repository hosts the Free Compiler.
   The Free Compiler is our compiler for the translation of non-strict languages (e.g., Haskell) with effects to strict languages (e.g., Coq) using free monads.
 - [haskell-src-transformations][] contains a prototypical pattern-matching compiler library that is used by the Free Compiler to transform Haskell programs with pattern matching on the left-hand side of function declarations into function declarations with explicit pattern matching using `case` expressions.
 - [language-coq][] is a Haskell package that provides a Coq AST and pretty-printer.
   This package is used by the Coq back end of the Free Compiler.
   The AST and pretty-printer has originally been developed as part of the [hs-to-coq][] compiler.
 - [free-proving-code][] is a library for modeling effectful programs in Coq in order to prove properties about these programs.
   Even thought the Free Compiler does not use this library directly, the model applied by the Free Compiler is based on the work that can be found in this repository.

This document aims to be as general as possible.
However, not everything that you can find here applies to all repositories.
Additional details may be provided in the contribution guidelines of the individual repositories.

## How Can I Contribute?

### Reporting Bugs

Bugs are tracked as [issues on GitHub][FreeProving/issues].
If you found a bug and determined which repository of the FreeProving project the bug is related to, first **make sure that the bug hasn't been reported yet** (see [Bugs][FreeProving/labels/bug]) and that you can reproduce the bug in the latest version of the compiler.
If the problem persists in the latest version and you cannot find a related bug report, create a new issue and provide as much of the following information as possible by filling out the *bug report* template.

 - Explain the problem and include additional details to help maintainers and members of the FreeProving project to reproduce the problem.

    + **Use a clear and descriptive title** for the issue to identify the problem.
    + **Describe the exact steps to reproduce the problem** in as much detail as possible.
      When listing steps, don't just say what you did, but explain how you did it.
    + **Provide specific examples to demonstrate the steps.**
      Try to find a minimal example that still shows the problematic behavior.
    + **Describe the behavior you observed after following the steps.**
    + **Explain which behavior you expected to see instead and why.**
    + **Include error messages and crash reports** reported by the compiler or operating system.

 - Include information about your configuration and environment.

    + **Which version of the repository are you using?**
      If you are using the Free Compiler, you can get the exact version by running `freec --version` in your terminal.
      Otherwise, run `git rev-parse HEAD` in your terminal in the repository's root directory to get the hash of the currently checked out Git commit.
    + **What's the name and version of the operating system you are using?**
    + **What versions of GHC and Cabal are you using?**
    + **How are you running the Free Compiler?** Have you installed the compiler as described in the README, are you running it using Cabal or do you use one of our Bash scripts?
       What command line arguments have you passed?
    + **If the problem regards generated or bundled Coq code,** what version of Coq are you using and how does your `_CoqProject` file look like (if any)?
    + **Have you made any modifications** to the source code or build configuration?

 - Assign the <kbd>bug</kbd> label to the issue.
   If you do not have the permission to add labels, a member of the FreeProving project will assign this label when reviewing the bug report.

### Suggesting Enhancements

Enhancement proposals are tracked as [issues on GitHub][FreeProving/issues].
If you want to propose an enhancement, first **make sure that there is no similar proposal already** (see [Enhancement Proposals][FreeProving/labels/enhancement]).
Consider leaving a comment or :+1: if you want to support an existing enhancement proposal.
If no such proposal has been made in the past, create a new issue and provide as much of the following information as possible by filling out the *feature request* template.

 - Explain the requested feature and include as much detail as possible to help maintainers and members of the FreeProving project understand your proposal.

    + **Use a clear and descriptive title** for the issue to identify the suggestion.
    + **Describe the current behavior** and **explain which behavior you would like to see instead** and why.
    + **Provide specific examples** to demonstrate both the current and wanted behavior.
    + **Explain why the enhancement is useful** to more users of the Free Compiler.
    + **List alternatives you have considered** and what's their drawback compared to your suggestion.

 - Assign the <kbd>enhancement</kbd> label to the issue.
   If you do not have the permission to add labels, a member of the FreeProving project will assign this label when reviewing the enhancement proposal.

### Contributing Code

In order to contribute code to the FreeProvig project, you have to submit a [pull request][FreeProving/pull-requests].
The following instructions guide you through the creation of a pull request and our quality assurance process.

 1. **Pick an issue to work on**

    - It is usually best to work on one issue at the time.
    - If you want to implement a feature but there is no issue yet, create a new issue first and consider discussing the change with other members of the FreeProving project first.
    - As a member of the free proving project, assign yourself to the issue you are currently working on to let others know that somebody is working on the issue already.
    - Take a look at the list of [good first issues][FreeProving/labels/good-first-issue] if you want to help but don't know where to start.

 2. **Create a fork or feature branch**

     - If you are not a member of the FreeProving project and want to contribute code, you have to fork the repository you want to contribute to on GitHub.
       Once you have created a fork, you can clone your fork and start making changes.

       ```
       git clone git@github.com:<YOUR_USER_NAME>/<REPOSITORY>.git
       ```

       In a forked repository, you can push to the master branch directly.
       Consider enabling GitHub actions on the Actions tab of your fork of the repository to run the CI pipeline before you create a pull request.

     - Members of the FreeProving project don't have to fork repositories they want to contribute to.
       In the main repository pushing to the master branch is prohibited.
       All development takes place in so called *feature branches*.
       If you are working on a specific issue `#N`, create a branch `issue-N` for all changes related to that issue.

       Run the following command to create and checkout a feature branch from the currently checked out branch.

       ```bash
       git checkout -b issue-N
       ```

 3. **Make changes**

    Make changes to the code in your fork or feature branch and commit the changes using [Git](#git).
    Prefer to make a lot of small changes and commit often instead of implementing the entire feature in one gigantic commit.
    Reference the issue you are working on in each commit message (see also the [styleguide for Git commit messages](#git-commit-messages)).

    Also consider the following when making changes.

    - Follow the applicable [styleguide](#styleguides).

    - Ensure that your changes work correctly and do not break other parts of the compiler by running [unit tests and other checks](#testing) frequently.
      You should also [write your own unit tests](#writing-unit-tests).

    - Pull in the master branch regularly to avoid merge conflicts later down the line.

      In a feature branch run the following command to merge the latest changes to the master branch on GitHub with your local (currently checked out) feature branch.

      ```bash
      git pull origin master
      ```

      If you are working on a fork, you have to add the original repository as a remote first.

      ```
      git remote add upstream git@github.com:FreeProving/<REPOSITORY>.git
      ```

      Now you can run the following command to merge the latest changes to the master branch of the original repository on GitHub with the local clone of your fork.

      ```bash
      git pull upstream master
      ```

    - When making user-facing or other notable changes, add a short entry to the "unreleased" section of the `CHANGELOG.md`.
      Explain the change briefly and in terms that a user can understand.

 4. **Create a pull request**

    Once you have implemented all changes and convinced yourself that everything is working as intend, you are ready to [submit a pull request][FreeProving/pull-requests/submit].
    If you are not fully done yet but want feedback on what you have done so far or need help for how to continue, you can also draft a pull request before.

    Provide the following information when submitting a pull request.

     - **Use a clear and descriptive title** for the pull request to summarize the changes.
     - **Describe *what* you have changed and *why* you had to change it.**
     - **Point out alternatives to your solution and potential drawbacks of your approach.**

 5. **Wait for all checks of the CI pipeline to run through**

    Whenever you open or reopen a pull request or push to the branch that is tracked by the pull request, a run of the [CI pipeline](#the-ci-pipeline) is triggered.
    A pull request must pass all checks in order to be accepted.
    If a check fails, try to identify and fix the problem.
    Once you push your fix, another run of the pipeline is triggered.
    Repeat this process until all checks pass.
    If you believe that the checks are failing due to an error in the CI pipeline configuration, leave a comment under your pull request asking a maintainer for help.
    A good first contact in those situations is [@just95][Maintainers/just95].

 6. **Wait for the pull request to be reviewed**

    A pull request must be reviewed by at least two members in order to be accepted.
    Reviewers may ask you to make additional changes, add test cases, update documentation or suggest improvements to your code before your pull request can be ultimately accepted.
    Implement the suggested changes, make sure the pipeline still passes and request another review when you are done and everything seems to work.
    Repeat this process until consent is met.

 7. **Wait for a maintainer to merge the pull request**

    Once consent is met and both reviewers approved the pull request, a project maintainer can merge the pull request.
    Ping a maintainer in a comment below your pull request, informing them that your pull request can be merged now.

    Like reviewers, a project maintainer may still request additional changes.
    If your branch has diverged far from the master branch, they may ask you to pull in the master branch and resolve potential merge conflicts.
    If they do not have any comments, they merge the pull request.

    After merging the pull request, the CI pipeline runs again.
    However this time the checks are performed against the master branch.
    It is not your responsibility anymore to make all checks pass in this final run of the CI pipeline.
    The maintainers are expected to take immediate action if the CI pipeline fails on the master branch.
    As a last resort, they may decide to revert the previously merged pull request.

## Additional Software

In addition to the required software listed in the README of the repository, you will need the following software to contribute code or documentation in the form of pull requests.

### Git

[Git][] is the version control system that we are using to manage code and documentation in this repository.
While simple changes (such as fixing typos in the documentation) can be performed directly via the [GitHub][] website, you have to [install Git][Git/Downloads] for anything more complex.
Git is mainly a command line tool, but graphical user interfaces are available, too.
An introduction to Git's command line interface can be found [here][Git/Tutorial].

### Tools for Haskell Development

We recommend installing the following tools if you want to contribute Haskell code.
Both of these tools are used to make sure that we are using a consistent code style throughout the project and are described in more detail in the [Haskell Styleguide](#haskell-styleguide) below.

 - [Brittany][software/Brittany], 0.12.1.1
 - [HLint][software/HLint], version 3.1.1

The versions mentioned above are the versions used by our [CI pipelines](#the-ci-pipeline).
Both tools must be installed in order to [run the CI pipeline locally](#running-the-pipeline-locally).
If you are not planning to make changes that involve the CI pipeline (i.e., modify Markdown documentation only), you do not have to install these tools.

## Directory Structure

In this section, we would like to give you a quick overview over the general structure of every repository that is part of the FreeProving project.
These guidelines standardize the organization of repositories such that you as a contributor can quickly find files you are looking for and confidently decide where to place files you want to add even if you are not familiar with the repository otherwise.
Repositories that deviate from these guidelines, contain additional top-level directories or want to provide more information on their directory structure should include additional information in their READMEs.

 - `./`

   The root directory of the repositories is home to important Markdown documents and central configuration files (e.g., Cabal configuration files).
   Avoid adding new files directly to the root directory if possible.
   Instead, select an appropriate subdirectory from the list below or create a new subdirectory if the file really does not fit any of the existing categories.

   If you create a new subdirectory, prefer singular (e.g., `example` not `examples`), lowercase (e.g., `example` not `Example`) and avoid abbreviations unless they are well known (e.g., `src` is a well known abbreviation of `source`).
   When in doubt, fully spell out the name!

 - `./.github`

   This directory contains GitHub related files such as issue and pull request templates as well as the configuration of the [CI pipeline](#the-ci-pipeline).
   Usually only project maintainers have to edit files in this directory.
   You can safely ignore it.

 - `./doc`

   This directory contains Markdown documentation of the software maintained in the repository.
   The documentation in this directory is mainly intended for users and not so much for developers.
   Documentation for more technical aspects, such as *module interfaces* and the *intermediate representation* of the Free Compiler for example, also belongs here.
   Nevertheless, avoid providing implementation details and don't require knowledge about internal workings of the implementation in these documents.

   Documents in this directory are named `[Title].md` where `[Title]` is the title of the Markdown document without spaces.

 - `./example`

   This directory contains example configurations or inputs for the software maintained in the repository.
   The examples should help users to get started with the software and demonstrate features as well as limitations.
   In case of the Free Compiler there are Haskell modules that can (or cannot) be compiled for example.
   More details about the examples and how to check out the examples should be provided in the repository's README.

 - `./img`

   This directory contains images that are embedded into the README or other Markdown documents.
   Usually you should avoid adding large binary files to Git repositories.
   Frequent changes to files in this directory should be avoided and new files should only be added if necessary.

 - `./src`

   This directory contains the source code of the software maintained in the repository.
   The contents of this directory are highly dependent on the type of software and programming language.

   If possible, the following three subdirectories should be distinguished.

    + `./src/exe` contains the code for the provided command line interface of the software or other executables (if any).
    + `./src/lib` contains the code for the library provided by the software or internal libraries that are necessary for the implementation of the executables.
    + `./src/test` contains test cases for the code located in `./src/lib`.

   In case of Haskell programs, all modules that belong to the repository should share a common prefix (e.g., `FreeC` for the Free Compiler).
   An exception to this rule are main modules such as `Main` and `Spec`.
   Furthermore, modules should be organized hierarchically based on their function.
   More details should be given in the repository's README.

 - `./tool`

   This directory contains Bash scripts for common actions that need to be performed during development.
   The scripts are intended to be executed from the root directory of this repository.

   ```bash
   ./tool/run.sh --help
   ```

   However, most scripts will make sure that they change into the correct working directory beforehand.
   For example, the Free Compiler runs in `/path/to/free-compiler` when invoked using the following command.

   ```bash
   /path/to/free-compiler/tool/run.sh ./example/Data/List.hs
   ```

   As a consequence `./example/Data/List.hs` refers to `/path/to/free-compiler/example/Data/List.hs` and not to `$(pwd)/example/Data/List.hs` in the example above.

   If there are other directories named `tool` in the repository, the contained scripts are interned to to be executed from the directory containing the `tool` directory by convention.

When adding files remember the following additional guidelines.

 - **Never commit generated code.**
   If you want to give an example for the software's output, commit the original file and provide instructions for how to obtain the generated code.
   If generated source code is used (e.g., code generated by a parser generator or a similar tool), update the build scripts to generate the code but do not commit the output.
   Best practice is to add all output file types and build directories to the `.gitignore` file in the root directory or an appropriate subdirectory such that generated code is not committed accidentally.

 - **Never commit secrets** such as private SSH keys.
   Once the commits are pushed the secret is publicly visible and compromised forever.
   Keys that are needed by the [CI pipeline](#the-ci-pipeline) (e.g., for deployment) are configured under `Settings > Secrets` on GitHub.

 - **Avoid to commit debugging code** that is only used for local debugging.
   Prefer to add real unit tests instead.
   You can temporarily commit code to debug a problem that can be observed in the [CI pipeline](#the-ci-pipeline) but not locally.
   However, you should make sure to remove such code once you are done debugging.

## Testing

Automated tests occupy a central role in our development and review process.
In this section we provide a quick overview over the general testing infrastructure, explain how you can run tests and give recommendations on how to write your own unit tests.

The instructions in this section are only applicable to repositories that contain Haskell source code.

> **Note:** Not all repositories in the FreeProving projects have unit tests at the moment.
> Thus, special care must be taken when making any changes to those repositories.
> Test your code manually with as many of the provided examples as possible.
> Contributions of automatic tests are welcome!

### Running Unit Tests

If you make changes to the code, you should run the unit tests to make sure that everything still works.
One option is to run the unit tests directly using Cabal via the following command.

```bash
cabal new-run tests -- [options...]
```

However, we recommend using the `./tool/test.sh` script for running unit tests during development instead which passes some handy default arguments to Cabal and the test suite.

```bash
./tool/test.sh [options...]
```

The most important difference is that the script overwrites GHC's `-Werror` flag with `-Wwarn`.
This allows the unit tests to run even if GHC reports warnings.
Doing so improves the development workflow.
Still remember to fix the warnings before creating a pull request since the [CI pipeline](#the-ci-pipeline) fails otherwise.

Furthermore, the script configures [Hspec][software/Hspec] (the library that we are using for testing) to create a failure report.
The failure report allows you to add the `--rerun` command line option to run test that failed in the previous run only.

```bash
./tool/test.sh --rerun
```

This allows you to focus on the failed test cases during debugging.
Once all tests are fixed, all tests are executed again.

More command line options are available.
Use the `--help` option for more information.

```bash
./tool/test.sh --help
```

### Writing Unit Tests

In addition to testing whether your changes do not break existing unit tests, we recommend writing your own test cases for every feature added or changed.

We are using the [Hspec][software/Hspec] testing framework for writing unit tests in Haskell.
For a module `FreeC.Foo` in `./src/lib` the module `FreeC.FooTests` in `./src/test/` contains the corresponding test cases.
Each test module should export one [`Spec`][software/Hspec/Spec] that [`describe`][software/Hspec/describe]s the tested module.
In tests of large modules, consider structuring your test cases by providing more [`context`][software/Hspec/context].

```haskell
-- | This module contains tests for "FreeC.Foo".

module FreeC.FooTests
  ( testFoo
  )
where

import           Test.Hspec

import           FreeC.Foo

-- | Test group for "FreeC.Foo" tests.
testFoo :: Spec
testFoo = describe "FreeC.Foo" $ do
  {- Write test cases here. -}
```

The exported `Spec` must be invoked by `./src/test/Spec.hs` or a `Tests.hs` module.

For every test case, the expected behavior is specified in a short sentence that usually starts with a verb in third-person.

```haskell
it "behaves as expected" $ do
  {- Implement test case here. -}
```

Test cases should be self contained and have as little dependencies on other components of the compiler as possible.
In case of the Free Compiler, modules starting with the [`FreeC.Test`][free-compiler/haddock/tests] prefix provide common utility functions for writing test cases more compactly.
Other repositories may choose a similar approach.
See the corresponding documentation for more details.

### The CI Pipeline

Whenever a pull request is opened, reopened or if you push to the branch that is tracked by an open pull request, a run of the continuous integration pipeline (CI pipeline) is triggered.
We are using [GitHub Actions][GitHub/Actions] for the CI pipeline.
You can find the corresponding workflow configuration file in `.github/workflows/ci-pipeline.yml`.

The CI pipeline of most repositories checks whether

 - the code has been formatted with [Brittany][software/Brittany]
 - [HLint][software/HLint] prints no hint that is not explicitly ignored in `.hlint.yaml`
 - the executable and the unit tests compile without warnings,
 - all unit tests pass and
 - Haddock generates the documentation without errors and there
   are no out of scope references in the documentation.

Additional check may be performed on the examples included in the `./example` directory.

If any check fails, the entire pipeline fails.
You will receive an email notification in this case.
A pull request cannot be merged unless the pipeline passed.

If a pull request does not modify the source code, examples, Cabal configuration or CI pipeline workflow file, the CI pipeline is not triggered.
This is for example the case when only Markdown documents have been edited.
The pull request can be merged as soon as all other requirements are met in this case.

### Running The Pipeline Locally

> **Note:** The instructions in this sections currently apply to the Free Compiler only.

Since a full run of the CI pipeline can take a while, you should make sure that all checks that are performed by the CI pipeline pass on your machine before you push your changes.
Luckily, you do not have to perform these checks manually, we provide a Bash script for that purpose.
Run the following command to simulate a run of the pipeline locally.

```bash
./tool/full-test.sh
```

The script usually runs much faster since there is no overhead for creating test environments, uploading and downloading artifacts, initializing caches etc.
If the script succeeds, it is not guaranteed that the CI pipeline will definitely pass, but it should catch the most common mistakes.

## Styleguides

In order to maintain a consistent code style, we try to adhere to the following guidelines for formatting, structuring and organizing our code in various languages.

If you are unsure how a piece of code should be formatted and the corresponding styleguide is not helping either, have a glance at existing source files to see how they handle similar situations, [open an issue][guidelines/issues] to start a discussion on the topic or [create a pull request][guidelines/pull-requests] to extend or clarify the styleguide in this document.
Furthermore, there is probably a lot of code in the individual repositories that violates the styleguides.
Don't hesitate to format the code accordingly and submit a pull request to the appropriate repository.

### Languages without Styleguide

We are using many different languages in this project.
There is Haskell code, Coq code, Bash scripts, Cabal, YAML and TOML configuration files, Markdown documents and many more to come in the future.
Unfortunately, there are not yet styleguides for all of those languages and for some there will probably never be one.
As always, you are of course encouraged to extend this document.
However, a compromise has to be found between the comprehensibility and completeness of this document.
At the moment, we do not see a need to add a style guide for script or configuration languages for example.
They make up only a very small fraction of the source code throughout the project and are not expected to be edited frequently by many different contributors.

If you have to work with a language for which no styleguide exist or you don't find any reference files for in any repository, use your best judgment and keep the following two main goals in mind.

 1. **Consistency**

    Format your code based on how other files of the same format are formatted.
    Most importantly, don't mix completely different styles in the same file, though.

 2. **Readability**

    Format your code such that it can be parsed and understood by a human reader easily.
    Readability is more important than consistency.
    Don't format your code such that it is absolutely unreadable just to conserve a consistent style with the way other code was formatted.
    However, that does not mean that you can use the argument of readability to sacrifice consistency whenever you feel like it.
    There is a trade off between readability and consistency!

Also the general rules discussed in the next subsection might help in such a situation.

### General Guidelines

The following general guidelines apply in every language if not noted otherwise in the styleguide for the language in question.

 - **Use UTF-8 encoded text files**

   All text files (i.e., source code, Markdown documents, configuration files etc.) should be UTF-8 encoded if not demanded otherwise by the corresponding language specification.

 - **Use spaces, not tabs**

   Use spaces to indent your code instead of tabs.
   The display width of a tab character varies from editor to editor and from configuration to configuration.
   As a result, you can never be sure that everybody sees all files the same way when tabs are used in a collaborative project.
   When using spaces, it is guaranteed that the code lines up as the original author intended everywhere.

   If not specified otherwise, we are using two spaces for indentation.
   If you prefer using the tab key of your keyboard, consider configuring your editor accordingly.

 - **Use Unix line endings**

   On Unix-like operating systems a line feed character (LF) is used to encode the end of a line while Microsoft Windows uses a carriage return followed by a line feed (CRLF) for line endings.
   When code is committed to this repository, it should use Unix line endings.
   If you are on a Windows machine, you can configure configure Git to automatically convert LF to CRLF when you check out code and back when you commit using the [following command][Git/Config/autocrlf].

   ```bash
   git config --global core.autocrlf true
   ```

 - **Avoid trailing whitespace**

   There should be no redundant trailing whitespace characters at the end of a line.

   In some formats (e.g., Markdown), trailing whitespace characters do have a special meaning.
   In such cases it is okay to include the trailing whitespace.

   ```markdown
   There are two spaces at the end of this line.  
   The two spaces at the end of the previous line cause a line break before this sentence in Markdown.
   ```

 - **Include newline at end of file**

   There should be a line ending character sequence (LF or CRLF on Windows) at the end of every source file if permitted by the file format.
   Without trailing newlines commands such as `cat` behave unexpectedly.

 - **Avoid redundant newlines**

   It is good practice to insert blank lines to group related code.
   For example, you should **DO** the following.

   ```bash
   # This is one group of code.
   foo
   bar

   # This is another group of code.
   # It is separated from the previous group by a blank line.
   baz
   qux
   ```

   However, you should not use multiple consecutive newline characters for such purposes.
   For example, you should not do the following.

   ```bash
   foo # This is one group of code.

   bar # This is another group of code which is slightly related to `foo`.
   ```


   baz # This is a group of code which is neither related to `foo` nor `bar`.
   ```

   Larger groups of code should be set apart using comments like the following.

   ```bash
   ###########################################################################
   # Some Heading for `foo` and `bar`                                        #
   ###########################################################################

   foo # This is one group of code.

   bar # This is another group of code which is slightly related to `foo`.

   ###########################################################################
   # Some Heading for `baz`                                                  #
   ###########################################################################

   baz # This is a group of code which is neither related to `foo` nor `bar`.
   ```

 - **Wrap lines after 80 characters**

   Long lines of text and source code are difficult to scan for the human eye and thus should be avoided.
   In case of [Markdown](#markdown-styleguide) documents, we do not have to deal with this problem since text can usually be soft wrapped without changing its meaning.
   In case of structured text such as source code, automatic line wrapping is not a good strategy for dealing with long lines.
   Thus, long lines should be hard wrapped such that structure, indentation and alignment are preserved with respect to syntax and semantics of the source code.
   The goal is to enhance readability, avoid horizontal scrolling and eliminate the need for resizing editor windows.

   One exception to this rule are links.
   If an URL does not fit into the current line, consider placing it on a line by itself but never insert a line break into the URL.
   It should be easy for the URL to be copied to the clipboard or automatically recognized by software.

   Line ending characters do not count towards the line length limit.

 - **Comment your code**

   + Good comments describe *what* your code does and *why* it does so.
     Avoid comments that simply reiterate *how* your code works.
     If the reader is interested in implementation details, they can refer to the code itself.
     However, the code will not teach them anything about your though process, theoretical understanding or hidden assumptions.

   + Every source file should start with a comment that states the purpose and contents of the file and how to use it.

   + At the very least every function and data type that is part of your code's public interface should be documented.
     However, also internal functions and data types should to be documented.

   + Inside functions you do not have to comment individual lines of code.
     It is usually best practice to split the code into small chunks with a well defined purpose and summarize what the code does and why it is necessary.

   + Use [Markdown](#markdown-styleguide) to format your comments if not specified otherwise.

   + Write in proper sentences.
     The first word in every comment should be capitalized.
     The comment should end with a period or other punctuation mark.

### Git Commit Messages

When writing Git commit messages, try to follow the following recommendations on [How to Write a Git Commit Message][GitCommit].

 - **Separate subject from body with a blank line**

   The commit message should start with a subject line that is separated from the rest of the commit message by a blank line.
   The subject line briefly summaries the changes in preferably 50 to at most 72 characters or less.

   ```
   Summarize changes using Markdown for formatting

   Give a more detailed explanation of the changes made by this commit in the
   body of the commit message. This explanation can span multiple lines or even
   paragraphs. This text is formatted using Markdown as well.
   ```

 - **Capitalize the subject line**

   The first word of the subject line should be capitalized (e.g. `Add feature XYZ` instead of `add feature XYZ`).

 - **Do not end the subject line with a period**

   Even though subject lines should form a sentence, trailing punctuation does not add any information and costs precious space.

 - **Use the present tense and imperative mood in the subject line**

   You should be able to read a Git commit message as "If applied, this commit will [subject]".

    + **DON'T:** `Added feature XYZ` or `Fixes #123`

    + **DO** `Add feature XYZ` or `Fix #123`

 - **Wrap lines at 72 characters**

    + One exception to this rule are links.
     Never wrap long links.
     Instead consider placing them on a line by themselves.
     This way, the links can be copied easily and can be recognized by terminals as clickable if such a feature is supported.

    + The subject line should be kept even shorter at below 50 characters if possible.
      You can exceed this limit if needed.
      However, the 72 characters should be considered a hard limit for the subject line.

 - **Reference issues and pull requests**

   If you are currently working on an issue or pull request, reference the number of the issue or pull request directly after the subject line.

    + `Add feature XYZ #42`
    + `Fix #42`

   If your change is related to multiple issues or pull requests, mention all of them.
   References to issues and pull requests don't count towards the line length limit.

    + `Add feature XYZ #42 #95`
    + `Fix #42 #95`

   Issues and pull requests from other repositories should not be referenced in the first line.
   Include the full link to the issue or pull request in the body of

   ```markdown
   Change something important #42

   As discussed in https://github.com/FreeProving/other-repository/pull/1,
   a change had to be made to this repository instead.
   ```

 - **Use Markdown to format your commit messages**

   If you want to format your commit messages use Markdown (for example, use [code spans][Markdown/code-spans] to format identifiers).
   The [Markdown Styleguide](#markdown-styleguide) applies but the rules above take precedence.
   For example, lines in Git commit messages are wrapped at 72 characters while they are not wrapped in Markdown documents.
   Also: just paste links into the commit message's body.
   There is no need for link reference definitions or links with text in commit messages.

- **Explain *what* and *why* something has been done and not *how***

- **The language of Git commit messages is English**

### Haskell Styleguide

The vast majority of the code in all repositories of the FreeProving project is written in Haskell.
We are using automatic code formatters and linters to enforce a consistent code style across the code base.
The tools we are using are covered by the subsections below.
The following is a list of additional guidelines that are not yet covered by the tools.

 - **Separate imports of internal and external modules**

    + The import declarations for modules from other packages should precede all imports of modules from this repository.
      The two blocks of import declarations are separated by a blank line.

      ```haskell
      import           Control.Monad
      import           Data.List

      import           FreeC.Environment
      ```

    + If you are hiding imports from the `Prelude` module, separate the corresponding `import` declaration from all other imports by a blank line.
      Sort the explicit import of the `Prelude` before all others.

      ```haskell
      import           Prelude                 hiding ( fail )

      import           Control.Monad.Fail             ( MonadFail(..) )
      import           Control.Monad.State            ( MonadState(..) )
      ```

 - **Sort imports alphabetically**

    + Within the individual blocks of import declarations, the imports are sorted alphabetically by the name of the imported module.

      ```haskell
      import           Control.Monad
      import           Data.List
      ```

    + If a module is imported qualified and unqualified, the unqualified import goes first.

      ```haskell
      import           Data.Set                       ( Set )
      import qualified Data.Set                      as Set
      ```

    + If the name of a module is prefixed with the name of another imported module, sort the module with the shorter name first.

      ```haskell
      import           Data.Set                       ( Set )
      import           Data.Set.Ordered               ( OSet )
      ```

 - **Use qualified imports**

   The `.hlint.yaml` file lists common aliases for modules.
   All of these modules should be imported `qualified` and `as` the corresponding alias.

   For example, the module `Data.Set` should always be imported as follows.
   Do not chose a different alias or omit the alias.

   ```haskell
   import qualified Data.Set                      as Set      -- DO
   import qualified Data.Set                      as S        -- DON'T
   import           Data.Set                                  -- DON'T
   ```

   It is allowed to import selected data types and operations explicitly from such modules.

   ```haskell
   import           Data.Set                       ( Set
                                                   , (\\)
                                                   )          -- OKAY
   ```


 - **Align constructors of data type declarations**

   If the constructors of a data type declaration do not fit on one line, align them as follows.

   ```haskell
   data Tree a
     = Leaf a
     | Branch (Tree a) (Tree a)
    deriving (Eq, Show)
   ```

   The constructors are indented by two spaces and the `deriving` clause is indented by a single space.

 - **Align fields of record constructors**

   In record constructors, each field is listed on it's own line.
   The type signatures are aligned.

   ```haskell
   data Person = Person
     { firstName :: String
     , lastName  :: String
     , age       :: Int
     }
    deriving (Eq, Show)
   ```

   If there is just a single field (e.g. in a `newtype` declaration) you can write the entire data type on one line if it fits.

   ```haskell
   newtype State s a = State { runState :: s -> (a, s) }
   ```

   The `deriving` clause still belongs on its own line and is indented by a single space.

 - **Add type signatures for all function declarations**

   Function declarations at top-level and in `where` clauses should have a type signature.
   The type signature should precede the function declaration immediately.
   No type signatures are needed in `let` bindings.

   If you cannot specify the type of a locally defined function due to type variable scoping rules, write the type in a block comment.
   The usage of block comments helps to distinguish type signature comments from Haddock comments.

   ```haskell
   foo :: a -> ((a, a), (a, a))
   foo x = (xx, xx)
     where {- xx :: (a, a) -}
           xx = (x, x)
   ```

 - **Naming conventions**

   + Use *lowerCamelCase* for function and variable names

   + Use *UpperCamelCase* for data type, constructor and class names

   + Don't define symbolic infix identifiers

     You shouldn't add functions or constructors with symbolic names such as `(|>)` or `(:<)`.
     A regular identifier are more descriptive.
     You can still use infix notation for custom functions and operators that are defined in external libraries.

     ```haskell
     x `foo` y  -- Custom function 'foo' in infix notation.
     xs :+: ys  -- Third-party operator ':+:' in infix notation.
     ```

 - **Grouping source code**

   The code in a module can often be further divided into groups of declarations with a similar intent.
   For example, a module that defines a data type often contains the actual data type definition, smart constructors, selectors, type class instances and so on.
   Include comments of the following format to set such groups of code apart.

   ```haskell
   -------------------------------------------------------------------------------
   -- Heading                                                                   --
   -------------------------------------------------------------------------------
   ```

   The comment contains a heading (such as "Smart Constructors") that concisely summarizes the intent of the code below.
   Before and after the comment with the heading, there should be a comment that contains 79 `-` characters.
   If the comment does not start in the first column of the source file, there may be fewer dashes to satisfy the 80 character limit per line.
   There are two trailing dashes at the end of the heading comment which align with the last two dashes of the other two comments.

#### Brittany

[Brittany][software/Brittany] is a code formatter for Haskell.
It can be installed via Cabal as follows.

```haskell
cabal new-install brittant
```

The [CI pipeline](#the-ci-pipeline) runs `brittany` on all Haskell source files in the `src` and `example` directories and compares its output with the committed files.
If there are Haskell source files that have not been formatted using `brittany`, the CI pipeline fails.
The same check is performed by the `./tool/check-formatting.sh` and `./tool/full-test.sh` scripts.

There is Brittany support for various editors (see also [Editor Integration][software/Brittany#editor-integration]).
If your editor is not supported, you can use the following shell script that we provide.

```haskell
./tool/format-code.sh [files...]
```

If no files are specified, all Haskell source files in the `src` and `example` directory are formatted by default.
Note that the script overwrites the formatted files.
Thus, you should create a backup beforehand by `git add`ing your changes, for example.

Of course Brittany is not perfect.
Among others, data type declarations are not formatted at the moment.
So don't rely entirely on the output of our automatic tests and manually check your code nonetheless according to the rules outlined above.

#### HLint

[HLint][software/HLint] is a tool that gives suggestions on how to improve Haskell source code.
It can be installed via Cabal as follows.

```haskell
cabal new-install hlint
```

The [CI pipeline](#the-ci-pipeline) runs `hlint` on all Haskell source files in the `src` directory.
If HLint has suggestions for how the code can be improved, the CI pipeline fails.
The same check is performed by the `./tool/full-test.sh` script.

There are HLint plugnis for many editors.
If there is no such plugin for your editor, you can run the following command instead.

```haskell
hlint src
```

Remember, that HLint only makes suggestions and you don't have to follow these suggestions.
However, since the CI pipeline fails if HLint finds possible improvements, hints have to be ignored explicitly.
Edit the `.hlint.yaml` file for this purpose and leave a comment why you had to ignore that hint.
Try to be as specific as possible when ignoring hints.

### Haddock Styleguide

Documentation for the Haskell code is written in [Haddock][software/Haddock] notation.

 - **Use Haddock for all Haskell comments**

   Even if a function is not exported by a module, it should have a comment in Haddock notation.

   ```haskell
   -- | The documentation for the module is written using Haddock.
   module Foo
     ( foo
     )
   where

   -- | 'foo' is exported and documented using Haddock.
   foo :: …
   foo = …
    where
     -- | 'bar' is defined locally but documented using Haddock anyway.
     bar :: …
     bar = …

   -- | 'baz' is not exported but documentation is written using Haddock
   --   nevertheless.
   baz :: …
   baz = …
   ```

   In non-documentation comments, Haddock markup should be used as well.
   For example, the following is not a Haddock comment, but `'name'` is used to refer to the variable `name`.

   ```haskell
   greet = do
     name <- getLine
     -- Print greeting for the 'name' entered by the user.
     putStrLn ("Hello, " ++ name ++ "!")
   ```

 - **Don't use block comments for Haddock**

   Always use line comments for documentation comments.

   ```haskell
   {-| DON'T DO THIS!

       Even though this syntax is more convenient sometimes,
       Haddock comments should never be written in Haskell's
       nested-comment style.
    -}
   ```

   Block comments should only be used to comment otherwise valid Haskell code out.

 - **Start Haddock comments with a single-sentence summary**

   The first paragraph of a Haddock comment should contain a single sentence that summarizes what the documented function, data type, type class etc. does or is intended for.
   The following paragraphs provide more detail.

   ```haskell
   -- | Concatenates the given lists.
   --
   --   The returned list contains all elements of the first list followed
   --   by all elements of the second list.
   append :: [a] -> [a] -> [a]
   append xs ys = …
   ```

   Documentation for modules don't have to start with a single sentence.
   However, the first paragraph should provide a brief summary of the contents and the purpose of the module.

 - **Start function comments with a third-person verb**

   The comment of a function declaration should answer the question "What does this function do?" by completing the sentence "This function ...".

   ```haskell
   -- | Tests whether all elements in the given list satisfy the
   --   given predicate.
   all :: [a -> Bool] -> [a] -> Bool
   all p xs = …
   ```

 - **Start variable binding and data type comments with a noun phrase**

   The comment of a variable binding or data type declaration should answer the question "What is this variable/data type?" by completing the sentence "This variable/data type is ...".

   ```haskell
   -- | The data type used to represent identifiers.
   type Identifier = String

   -- | The prefix names of QuickCheck properties start with by
   --   convention.
   prefix :: Identifier
   prefix = "prop_"
   ```

 - **Align text with the comment's first character**

   ```haskell
   -- | If a comment spans multiple lines
   --   all following lines should be aligned
   --   with the first character of the comment.
   --
   --   Additional paragraphs are also aligned
   --   with the first character of the comment.
   ```

 - **Use "bird tracks" for code snippets**

   In Haddock there are two ways of writing code blocks: by surrounding a paragraph with `@...@` or by preceding each line of a paragraph with `>` ("bird tracks")

   ```haskell
   -- | @
   --   show Foo = "Foo"
   --   @
   --
   --   and
   --
   --   > show Foo = "Foo"
   ```

   The important difference is that in the `@...@` form, markup is interpreted as usual inside the code block while the text after `>` is interpreted literally.
   In the example with `@...@` above, `"Foo"` is a link to the module `Foo` whereas it is just the text `"Foo"` in the example with `>`.
   As this behavior is not expected (and it is too easy to forget to escape some characters), you should always use the `>` notation.

   Unfortunately, there is no inline equivalent for `>`.
   Thus, we have to use `@...@` for inline code.
   Remember to escape all characters that have a special meaning in Haddock markup.

 - **Prefer Unicode over LaTeX**

   If you have to use mathematical symbols (e.g. Greek letters or subscripts) in your comments, try to use Unicode characters (e.g., `α` or `xₙ`) instead of embedding LaTeX code into the documentation (e.g. `\(\alpha\)` or `\(x_n\)`).
   While LaTeX produces more readable formulas in the generated HTML version of the documentation, the excessive use of LaTeX reduces the readability of the comments in the source code itself.

   Most editors or operating systems have support for typing Unicode characters directly with the keyboard.

### Markdown Styleguide

While Haddock is used to document the Haskell source code, we are using [Markdown][Markdown] to write the remaining documentation.
Markdown is also used in commit messages and comments of all other languages (e.g., in Bash scripts) if not specified otherwise.
When writing markdown documents adhere to the following style considerations.

 - **Write one sentence per line**

   Unlike in source code, long lines of Markdown should not be wrapped.
   By writing one sentence per line, versioning the Markdown files gets easier.
   If lines are wrapped, whole paragraphs sometimes need to be relayouted even when just a single word was changed which obfuscates diffs unnecessarily.

   We still recommend enabling the soft wrapping feature (preferably at a line length of 80 characters) of your editor to avoid horizontal scrolling.

 - **Use ATX headings**

   There are two ways of writing headings in Markdown: ATX and Setext headings.

   ```markdown
   # This is an ATX Heading

   This is a Setext Heading
   ========================
   ```

   We prefer the usage of ATX headings.
   Their key advantage over Setext headings is that there are up to six levels of nesting as opposed to two.

    + Your document should start with a level one ATX heading.
      This heading contains the title of the document.
      There should be only one of those headings in the entire document.
    + Start each section of your document with its own level two ATX heading and add as many subsections at level three or deeper as necessary.
    + Avoid having a single subsection for a section (except if you have plans to add further items down the line).
    + Avoid two consecutive headings.
      Consider writing a short introduction to the section in this case.
    + Capitalize the first word of the heading (e.g. "The CI Pipeline" instead of "the CI Pipeline").
    + Capitalize all other words except for articles, conjunctions and prepositions (e.g. "How Can I Contribute?" instead of "How can I contribute?" but "Haskell to Coq" instead of "Haskell To Coq").

   ```markdown
   # Document Title
   ## Section 1
   ## Section 2
   ### Subsection 2.1
   ### Subsection 2.2
   ## Section 3
   ### Subsection 3.1
   ### Subsection 3.2
   #### Subsection 3.2.1
   #### Subsection 3.2.2
   ```

 - **Add a table of contents to long document**

   Markdown documents with many sections and subsections can get very difficult to navigate quickly.
   If you cannot break up the document into multiple files, consider adding a table of contents.

    + The table of contents should be the first section of a document.
    + Write a short description or introduction before the table of contents.
    + Don't list the table of contents in the table itself.
    + Avoid move than three levels of nesting.
      Two levels are preferred.
    + Every item of the table should be a link to the corresponding section or subsection.
      The link text should be the same as in the heading of the section.
      GitHub automatically generates an anchor for every heading in the document.
      Just use that anchor in the link, don't use the full address and don't use [link reference definitions][Markdown/link-reference-definition] for internal references.

   ```markdown
   # Document Title

   <short introduction>

   ## Table of Contents

   1. [Section 1](#section-1)
   2. [Section 2](#section-2)
       1. [Section 2.1](#section-2-1)
       2. [Section 2.2](#section-2-2)
   3. [Section 3](#section-3)
       1. [Section 3.1](#section-3-1)
       2. [Section 3.2](#section-3-2)
           1. [Section 3.2.1](#section-3-2-1)
           2. [Section 3.2.2](#section-3-2-2)
   ```

 - **Use link reference definitions for external links**

   If you have to link to external resources, don't write the URL directly in the text.
   Instead maintain all references in the form of [link reference definitions][Markdown/link-reference-definition] at the bottom of the document.

    + Make sure to give a concise name to each reference and include the title of the page you are linking to as the link label.
    + The list of link reference definitions should be sorted alphabetically.
    + Split the list of link reference definitions into logical blocks if necessary.

   ```markdown
    [doc/ModuleInterfaceFileFormat.md]:
      https://github.com/FreeProving/free-compiler/blob/master/doc/ModuleInterfaceFileFormat.md
      "Module Interface File Format — Free Compiler Documentation"

    [wiki/ANSI]:
      https://en.wikipedia.org/wiki/ANSI_escape_code
      "ANSI escape code — Wikipedia"
    [wiki/Unicode]:
      https://en.wikipedia.org/wiki/Unicode_subscripts_and_superscripts
      "Unicode subscripts and superscripts — Wikipedia"
   ```

   Inside the document you link to these resources as follows.

   ```markdown
   See this [wikipedia article][wiki/ANSI] for more information.
   ```

   Links of the form `[...](URL)` should be used for internal references only (i.e., to link to sections in the same document).

 - **Format and syntax highlight code snippets**

   When you use code snippets in your Markdown document (and you probably should be!) format the embedded source code as you would format any other source code.
   For example, if you have an example involving Haskell code, format that code using Brittany first.

   You should use [fenced code blocks][Markdown/fenced-code-blocks] rather than indented code blocks and specify the language of the embedded source code explicitly.
   For example, if you want to give an example hello world program written in Haskell, embed the source code as follows.

   ~~~Markdown
   ```haskell
   main :: IO ()
   main = putStrLn "Hello, World!"
   ```
   ~~~

   By specifying the language explicitly, GitHub automatically performs syntax highlighting for most languages.
   The example above should look as follows.

   ```haskell
   main :: IO ()
   main = putStrLn "Hello, World!"
   ```

   + Use `bash` as the default language of shell commands.

   + You may omit language specifiers when you just want to include a block of monospaced or pre-wrapped text (e.g., to show the output of a command).

 - **Use code spans for identifiers and filenames**

   If you have to refer to variables, functions, types, modules, files, small code fragments etc. in the text, use backticks (`` ` ``) to format them as [code spans][Markdown/code-spans].

   ```markdown
   DON'T: The append function defined in ./example/Data/List.hs
          corresponds to (++) from the Prelude.

   DO:    The `append` function defined in `./example/Data/List.hs`
          corresponds to `(++)` from the `Prelude`.
   ```

 - **Use block quotes to highlight important paragraphs**

   If you want to draw the users attention to an important paragraph (e.g., a notice or warning), this paragraph should be wrapped in a [block quote][Markdown/block-quotes].

    + The paragraph should start with a word like "Warning", "Note" or similar followed by a colon.
      The word and colon should be bold text.
    + Each line of the paragraph starts with a block quote marker (`>`).

   ```markdown

   > **Warning:** Never commit the private key to the Git repository!

   ```

   > **Remember:** Consider wisely when to use a such a paragraph and don't overdo it.
   > Most importantly, don't scare the user but inform them such that they can make their own decisions.

 - **Use different bullets for nested unordered lists**

   When nesting unordered lists, each level should use a different bullet (i.e., `-`, `+` or `*`) to make the nesting of the list more apparent from the Markdown source code.
   Prefer to use `-` for top-level lists, `+` for nested lists and `*` for lists that are nested one level deeper.
   Avoid more than three levels of nesting.
   The bullet points of unordered lists are indented by one space.

   ```markdown
    - This is a top-level list item.
       + This is an item of a nested list.
          * This is a very deeply nested list item.
          * Avoid nesting list items any deeper.
            - If you really have to, start with the `-` bullet again.
       + This item is at the first nesting level again.
    - This item is at top-level again.
   ```

## Leagal information

This section discusses the legal consequences of your contributions to the FreeProving project.
We know that legal topics can be tiresome.
However, we encourage you to carefully read this section nonetheless.
Please make sure that you understand and agree with all what's is written here before you contribute.

### Privacy

All repositories of the FreeProving project are developed and maintained on [GitHub][].
In order to contribute to the FreeProving project, you have to create a GitHub account.
By contributing to the FreeProving project, you agree that your contributions are published on GitHub.
GitHub's [terms of privacy][GitHub/Privacy] apply.

Note that if you contribute by the means of Git commits, your locally configured name and email address will be part of the commit message and permanently stored as part of the publicly visible commit history once you push your changes.
Of course, you are free to anonymise/pseudonymise your contributions to the extend permitted by applicable law and GitHub's [terms of service][GitHub/Terms].
We do not require you to provide any personal information.
If you chose to disclose personal information about your own person through your contributions nonetheless, you are doing so completely voluntarily and at your own risk.

Please respect the privacy of other project members and contributors.
If you have to mention another person, best practice is to use their GitHub user name instead of their real name even if you know them in person or their real name is publicly visible on their GitHub profile page.
See our [Code of Conduct][guidelines/CODE_OF_CONDUCT] for more information.

### License

The FreeProving project is an open source project.
The source code, associated documentation, configuration, toolchain and everything else you in the repositories of the FreeProving project is licensed under open source licenses such as [The 3-Clause BSD License][licenses/3-Clause-BSD] or [The MIT License][licenses/MIT].
By contributing to the FreeProving project, you agree that your contributions will be licensed under the same license.

In case of most open source licenses, this includes that your contributions can be

 - modified and distributed almost arbitrarily and
 - used royalty free for private or commercial purposes

by anyone provided that the requirements of the respective license regarding for example the attribution of the copyright holders are met.  
See the [LICENSE][guidelines/LICENSE] file of the corresponding repository for details.

[free-compiler]:
  https://github.com/FreeProving/free-compiler
  "Free Compiler on GitHub"
[free-compiler/haddock/tests]:
  https://freeproving.github.io/free-compiler/docs/master/freec-unit-tests/
  "Free Compiler Test Suite — Haddock Documentation"

[FreeProving/issues]:
  https://github.com/search?q=is%3Aopen+is%3Aissue+user%3AFreeProving+sort%3Acomments-desc
  "Free Proving — Issues"
[FreeProving/labels/bug]:
  https://github.com/search?q=is%3Aopen+is%3Aissue+label%3Abug+user%3AFreeProving+sort%3Acomments-desc
  "Free Proving — Issues — Bugs"
[FreeProving/labels/enhancement]:
  https://github.com/search?q=is%3Aopen+is%3Aissue+label%3Aenhancement+user%3AFreeProving+sort%3Acomments-desc
  "Free Proving — Issues — Enhancements"
[FreeProving/labels/good-first-issue]:
  https://github.com/search?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue%22+user%3AFreeProving+sort%3Acomments-desc
  "Free Proving — Issues — Good First Issue"
[FreeProving/pull-requests]:
  https://github.com/search?q=is%3Aopen+is%3Apr+user%3AFreeProving+sort%3Acomments-desc
  "Free Compiler — Pull Requests"
[FreeProving/pull-requests/submit]:
  https://github.com/FreeProving/guidelines/blob/master/doc/SubmitPullRequest.md
  "Free Compiler — Pull Requests"

[free-proving-code]:
  https://github.com/FreeProving/free-proving-code
  "free-proving-code on GitHub"

[Git]:
  https://git-scm.com/
  "Git"
[Git/Downloads]:
  https://git-scm.com/downloads
  "Git — Downloads"
[Git/Config/autocrlf]:
  https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration#_code_core_autocrlf_code
  "core.autocrlf — Git Configuration"
[Git/Tutorial]:
  https://git-scm.com/docs/gittutorial
  "Git — Tutorial"

[GitCommit]:
  https://chris.beams.io/posts/git-commit/
  "Chris Beams — How to Write a Git Commit Message"

[GitHub]:
  https://github.com/FreeProving
  "FreeProving on GitHub"
[GitHub/Actions]:
  https://github.com/features/actions
  "GitHub Actions"
[GitHub/Privacy]:
  https://help.github.com/en/github/site-policy/github-privacy-statement
  "GitHub Privacy Statement"
[GitHub/Terms]:
  https://help.github.com/en/github/site-policy/github-terms-of-service
  "GitHub Terms of Service"

[guidelines]:
  https://github.com/FreeProving/guidelines
  "FreeProving Guidelines on GitHub"
[guidelines/CODE_OF_CONDUCT]:
  https://github.com/FreeProving/guidelines/blob/master/CODE_OF_CONDUCT.md
  "FreeProving Guidelines — Code of Conduct"
[guidelines/issues]:
  https://github.com/FreeProving/guidelines/issues
  "FreeProving Guidelines — Issues"
[guidelines/LICENSE]:
  https://github.com/FreeProving/guidelines/blob/master/LICENSE
  "FreeProving Guidelines — LICENSE file template"
[guidelines/pull-requests]:
  https://github.com/FreeProving/guidelines/pulls
  "FreeProving Guidelines — Pull Requests"

[haskell-src-transformations]:
  https://github.com/FreeProving/haskell-src-transformations
  "haskell-src-transformations on GitHub"

[hs-to-coq]:
  https://github.com/antalsz/hs-to-coq
  "hs-to-coq on GitHub"

[language-coq]:
  https://github.com/FreeProving/language-coq
  "language-coq on GitHub"

[licenses/3-Clause-BSD]:
  https://opensource.org/licenses/BSD-3-Clause
  "The 3-Clause BSD License"
[licenses/MIT]:
  https://opensource.org/licenses/MIT
  "The MIT License"

[Maintainers/just95]:
  https://github.com/just95
  "Free Compiler — Issues"

[Markdown]:
  https://github.github.com/gfm/
  "GitHub Flavored Markdown Spec"
[Markdown/block-quotes]:
  https://github.github.com/gfm/#block-quotes
  "GitHub Flavored Markdown Spec — Block quotes"
[Markdown/code-spans]:
  https://github.github.com/gfm/#code-spans
  "GitHub Flavored Markdown Spec — Code spans"
[Markdown/fenced-code-blocks]:
  https://github.github.com/gfm/#fenced-code-blocks
  "GitHub Flavored Markdown Spec — Fenced code blocks"
[Markdown/link-reference-definition]:
  https://github.github.com/gfm/#link-reference-definition
  "GitHub Flavored Markdown Spec — Link reference definitions"

[software/Brittany]:
  https://github.com/lspitzner/brittany/
  "Brittany"
[software/Brittany#editor-integration]:
  https://github.com/lspitzner/brittany/#editor-integration
  "Brittany — Editor Integration"
[software/Haddock]:
  https://www.haskell.org/haddock/
  "Haddock"
[software/HLint]:
  https://github.com/ndmitchell/hlint
  "HLint"
[software/Hspec]:
  https://hspec.github.io/
  "Hspec: A Testing Framework for Haskell"
[software/Hspec/context]:
  https://hackage.haskell.org/package/hspec-2.7.1/docs/Test-Hspec.html#v:context
  "Test.Hspec — context"
[software/Hspec/describe]:
  https://hackage.haskell.org/package/hspec-2.7.1/docs/Test-Hspec.html#v:describe
  "Test.Hspec — describe"
[software/Hspec/Spec]:
  https://hackage.haskell.org/package/hspec-2.7.1/docs/Test-Hspec.html#t:Spec
  "Test.Hspec — type Spec"
