This plugin uses the [Gut](https://github.com/bitwes/Gut) test framework add-on for Godot to implement unit and integration tests. For advanced operation, review of Gut's extensive wiki is recommended. This document will describe the most basic usage patterns for this project.

_**Note:** This document can eventually be moved into the repository's wiki._

## Running Tests

The easiest way to run all of this project's unit and integration tests is from the [command line](https://github.com/bitwes/Gut/wiki/Command-Line). First, ensure that your shell has the `godot` alias defined. For example, one might add the following to their `~/.zshrc` file on macOS and then re-source (or simply restart) their shell session.

```bash
alias godot='/Applications/Godot.app/Contents/MacOS/Godot'
```

From here, the all tests can be executed and the Gut test console opened with the following command.

```bash
godot -d -s --path $PWD addons/gut/gut_cmdln.gd
```

## Creating Tests

Tests exist in the following directories.

- `/test/unit` holds small tests of specific units/components/classes/methods.
- `/test/integration` holds large tests of the entire plugin's functionality combined.

Gut has an extensive API for writing tests. Recommended reading includes its [Quick Start page](https://github.com/bitwes/Gut/wiki/Quick-Start) and its [Creating Tests page](https://github.com/bitwes/Gut/wiki/Creating-Tests).

### Notes, Best Practices & Guidelines

- The test suite is run from the command line via a GitHub Action for each pull request.
- In order to avoid memory leaks (which will cause major issues during our CI/CD pipelines), **all dynamically-instantiated nodes must be manually freed in tests**. This can be done by calling `queue_free()` on said nodes.