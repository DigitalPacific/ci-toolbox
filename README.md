# ci-toolbox

This toolbox contains popular PHP utilites used to ensure stability for continuous integration.

Within this package you will find a rabbit.yaml file which is used to run all the included utilites. Rabbit is an easy to install Python application [https://github.com/ouijan/rabbit](https://github.com/ouijan/rabbit).

## Install

Require the package in your `composer.json` file and run the `composer install` command to install it:

```json
{
    "require-dev": {
        "DigitalPacific/ci-toolbox": "0.*"
    }
}
```

Move the included rabbit.yaml file into the root directory of your application

## Usage

This toolbox is just a collection of popular PHP utilites with a convient way to run them using Rabbit.

```
$ cd /path/to/the/root/of/your/application
```

Once the rabbit.yaml file is in the root directory of your application and you have successfully [installed](https://github.com/ouijan/rabbit) Rabbit.

You can either run the entire utility suite:

```
$ rabbit utility-suite
```

or individual pieces:

```
$ rabbit lint
```

To see all the different rabbit commands for the project type:

```
$ rabbit
```