# ci-toolbox

This toolbox contains popular PHP utilities used to ensure stability for continuous integration.

Within this package you will find a rabbit.yaml file which is used to run all the included utilities. Rabbit is an easy to install Python application [https://github.com/ouijan/rabbit](https://github.com/ouijan/rabbit).

## Install - Package

Require the package in your `composer.json` file and run the `composer install` command to install it:

```json
{
    "require-dev": {
        "digital-pacific/ci-toolbox": "0.*"
    }
}
```

## Install - Rabbit

Rabbit is a Python module that can be installed via pip, visit Rabbit's [repo](https://github.com/ouijan/rabbit) for installation instructions.

Once Rabbit has been installed copy the appropriate yaml file from the rabbit folder into the root directory of your code. Rename the file rabbit.yaml.

If everything is installed correctly run:

```
$ rabbit
```

Which should display:

```
Usage: rabbit [OPTIONS] COMMAND [ARGS]...

Options:
  --help  Show this message and exit.

Commands:
  compliance
  duplicates     Uses PHPCPD to detect duplicate lines of code
  lint           Uses parallel-lint to parse the current...
  rules          Uses PHP Mess Detector to run code against...
  separator      Separator to go in-between different commands
  unittest       Uses PHPUnit to run unit tests on the...
  utility-suite  Complete testing suite.
```

## Install - Patch

This toolbox is just a collection of other utilities that have their own dependencies. One of those dependencies is a program called patch.

A patch program is already installed on OSX

Centos Installation:

```
$ yum install patch
```

Ubunutu Installation:

```
$ apt-get install patch
```

## Usage

This toolbox is just a collection of popular PHP utilities with a convenient way to run them using Rabbit.

There are 5 utilities in this toolbox:

- [php-parallel-lint](https://github.com/JakubOnderka/PHP-Parallel-Lint)
- [php_codesniffer](https://github.com/squizlabs/PHP_CodeSniffer)
- [phpcpd](https://github.com/sebastianbergmann/phpcpd)
- [phpmd](https://github.com/phpmd/phpmd)
- [phpunit](https://github.com/sebastianbergmann/phpunit)

The way that Rabbit is setup is to run each of these utilities individually or as a suite.

If you are importing this package into an existing project it is recommended that first run each utility individually, fixing up problems that are reported and tweaking the rabbit.yaml file to suite your projects needs before running the the entire suite of utilities.

Here is an example of how to run an individual utility:

```
$ cd /path/to/the/root/of/your/application
```

```
$ rabbit lint
```

Once you finished running the utilities individually you can run the entire suite by using:

```
$ rabbit utility-suite
```

This command runs each individual utility and exits with that utilities exit code. So if during the execution of this command the first utility has an exit code that is not 0 no other utilities will run after it. This is useful in a continuous integration environment where a script could call this single command to run the entire suite and be confident that if the suite exits with a code of 0 then everything has passed.

If you need a reminder of the different Rabbit commands already setup, you can either view the rabbit.yaml file or run:

```
$ rabbit
```

## Bitbucket Pipeline

Bitbucket has a new feature called Pipelines that this toolbox can be utilised for in your PHP projects.

A docker image has been created specifically for use with this toolbox and can be found at [php-ci-toolbox](https://hub.docker.com/r/gblankenship/php-ci-toolbox/).

An example bitbucket-pipelines.yml file for running this ci-toolbox is below.

```
image: gblankenship/php-ci-toolbox:latest
pipelines:
  default:
    - step:
        script:
          - composer -V
          - composer install
          - cp vendor/digital-pacific/ci-toolbox/rabbit/laravel.rabbit.yaml ./rabbit.yaml
          - rabbit utility-suite
```
