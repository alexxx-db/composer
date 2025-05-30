# Contributing to Composer

Thanks for considering contributing to Composer!

Issues tagged with [good first issue](https://github.com/mosaicml/composer/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22) are great options to start contributing.

If you have questions, join us on [Slack](https://join.slack.com/t/mosaicml-community/shared_invite/zt-w0tiddn9-WGTlRpfjcO9J5jyrMub1dg) -- we'll be happy to help you!

We welcome contributions for bug fixes, new efficient methods you'd like to contribute to the community, or new models and datasets!

## New Algorithms

Have a new algorithm you'd like to contribute to the library as part of your research? We welcome any PRs, and recommend filing an issue with the proposed method or reaching out on Slack first!

## Prerequisites

To set up the development environment in your local box, run the commands below.

1\. Install the dependencies needed for testing and linting the code:

<!--pytest.mark.skip-->
```bash
pip install -e '.[all]'
```

2\. Configure [pre-commit](https://pre-commit.com/), which automatically formats code before
each commit:

<!--pytest.mark.skip-->
```bash
pre-commit install
```

## Submitting a Contribution

To submit a contribution:

1\. Fork a copy of the [Composer](https://github.com/mosaicml/composer) library to your own account.

2\. Clone your fork locally and add the mosaicml repo as a remote repository:

<!--pytest.mark.skip-->
```bash
git clone git@github.com:<github_id>/composer.git
cd composer
git remote add upstream https://github.com/mosaicml/composer.git
```

3\. Create a branch and make your proposed changes.

<!--pytest.mark.skip-->
```bash
git checkout -b cool-new-feature
```

4\. When you are ready, submit a pull request into the composer repository! If merged, we'll reach out to send you some free swag :)

## Pull request (PR) guidelines

We have some rough guidelines that will make your PR easier to review and more likely to get smoothly merged. Please don't let uncertainty or difficulty with any of these things stop you from opening a PR! We are happy to help you through them :)
* Self-contained title and description. Please include a concise title and clear PR description. The title should allow someone to understand what the PR changes or does at a glance. The description should allow someone to understand the contents of the PR _without_ looking at the code.
* If the PR affects output that is displayed to a user of Composer (e.g. console logging or experiment tracker reporting), please include screenshots showing what the new output looks like. UX is important!
* Include tests. If you are fixing a bug, please add a test that would've caught the bug. If you are adding a new feature, please add unit tests that test the various components of the feature, and also a test that tests the full functionality of the feature.
* Please consider whether your changes affect the example notebooks or large parts of the code base, and run the daily tests locally if so (`pytest -m 'daily and not remote and not gpu and not vision and not doctest'`)
* `pre-commit` should help you handle formatting and type checking, but please do make sure you have it installed as described [above](#prerequisites).

## Configuring README Code Snippets

Composer uses [pytest-codeblocks](https://github.com/nschloe/pytest-codeblocks) to test all example code snippets. The pytest-codeblocks repository explains how to annotate code snippets, which supports most `pytest` configurations. For example, if a test requires model training, the GPU mark (`<!--pytest.mark.skip-->`) should be applied.

## Running Tests

To test your changes locally, run:

* `make test`  # run CPU tests
* `make test-gpu`  # run GPU tests
* `cd docs && make doctest`  # run doctests

Some of our checks test distributed training as well. To test these, run:

* `make test-dist WORLD_SIZE=2`  # run 2-cpu distributed tests
* `make test-dist-gpu WORLD_SIZE=2`  # run 2-gpu distributed tests

These tests run with the `composer` launcher. We also support `WORLD_SIZE=1`, which would run the tests with the `composer` launcher on a single device.

See the [Makefile](/Makefile) for more information.

If you want to run pre-commit hooks manually, which check for code formatting and type annotations, run `pre-commit run --all-files`

### Docker
To run the tests in the provided docker containers:

* `docker pull mosaicml/composer` (or an alternative image like `mosaicml/composer:latest_cpu`)
* `docker run --rm -v ./:/composer --user $(id -u):$(id -g) -it mosaicml/composer`
* from inside the container
    * `cd /composer`
    * `pip install -e .`
    * `pytest <args>` or `make <args>` to run the desired tests

### Checking documentation

If your changes affect the documentation, please get a chance to build the docs locally and view it to verify if the changes
are what you wanted.

<!--pytest.mark.skip-->
```bash
cd docs
pip install -e '.[docs]'
make clean && make html
make host   # open the output link in a browser.
```


## Code Style & Typing

See the [Composer Style Guide](/STYLE_GUIDE.md) for guidelines on how to structure and format your code.

Composer aims to annotate all functions with type annotations (introduced in
[PEP 526](https://www.python.org/dev/peps/pep-0526/)). Don't worry if you are not a Python typing expert;
put in the pull request, and we'll help you with getting the code into shape.
