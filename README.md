---
permalink: /
title: Dev-Nanny
---

The Dev-Nanny project is aimed to make it trivial for developers to improve the
quality of the code they write, regardless of experience level.

This primary goal is supported by tools that offer education and enforcement.
As Dev-Nanny uses various tools to help her make suggestions or improvements, the
definition of "quality" can be defined by the programmer.

However, if a programmer finds it difficult to define "quality", dev-nanny will
make a suggestion there too.

This makes DevNanny ideally suited for both novice programmers as well as
seasoned professionals.

## Usage

Everything should work straight out of the box. DevNanny will be run each time
a developer does a `git commit`.

After the next release of Dev-nanny, it can also be run from the command-line using the binary placed in the
`vendor/bin` folder. The full command would be:

    ./vendor/bin/dev-nanny

On each run, all included connectors will be run.

## Installation

Dev-Nanny needs to be installed per individual project using Composer.
If Composer is not (yet) installed, do so before proceeding, follow the [Composer installation instructions].

Run the following command on the command-line inside your project folder:

    php composer.phar require dev-nanny/dev-nanny --dev

This will download everything Dev-Nanny needs and install the git hook.

### Available Connectors

Connectors are available for the following tools:

 - [Php Lint][Connector-PhpLint] (also known as `php -l`)

Planned Connectors:

 - Config Checker (compares config files of various services against DevNanny/Config
   package and make suggestions for improvement)
 - Other Lints (js, css, yml, scss, xml, bash, etc.)
 - QA Tools (CodeSniffer, Copy/Paste Detector, Mess Detector, etc.)
 - Test Runners (PhpUnit, Behat, Codeception, PhpSpec, etc.)

## What's in the box?

### Packages

This project has been divided into separate packages that each have a single,
distinct, responsibility. This is done to make it as easy as possible to alter,
overwrite or customise parts of DevNanny.

- [Dev-Nanny] - Meta Package
- [ComposerPlugin]
- [ConnectorBase]
- [Connectors] - Meta Package
- [GitHook]

The chain of dependency is as follows:

       Dev-Nanny/Dev-Nanny¹ ---> Dev-Nanny/ComposerPlugin² ---> Dev-Nanny/GitHook
                    |
                    `-> Dev-Nanny/Connectors¹ ---> Dev-Nanny/ConnectorBase
                                               `-> Individual Connectors³
    ¹ = Meta Package
    ² = Composer Plugin
    ³ = Dev Nanny Connector

## Trouble Shooting /FAQ

### What if I don't use `git` but `SVN`/`Mercurial`/`Bazaar`/etc.?

You will need to create an appropriate hook yourself. It will need to run
DevNanny against the received file list. (See the *Usage* section)

If you decide to create such a hook, please share the result so others may also
benefit from your efforts.

If creating a hook seems too complex or daunting, feel free to open an issue
requesting an example or full implementation.

### What if I don't use *any* versioning tool?

If you don't use any versioning tool *ever* you may want to consider starting to
use one *now*. You are missing out on great things!

If you don't use a versioning tool for a certain project, you can always just
run dev-nanny occasionally by hand or use a file-watcher or task-runner to run
dev-nanny on an interval or whenever a file changes.

[Dev-Nanny]: https://github.com/dev-nanny/dev-nanny/
[ComposerPlugin]: https://github.com/dev-nanny/ComposerPlugin/
[GitHook]: https://github.com/dev-nanny/GitHook
[Connectors]: https://github.com/dev-nanny/Connectors/
[ConnectorBase]: https://github.com/dev-nanny/Connector-Base
[Connector-PhpLint]: https://github.com/dev-nanny/Connector-PhpLint/
[Composer installation instructions]: https://getcomposer.org/doc/00-intro.md
