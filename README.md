# Dev Helper Commands

Useful commands for every Developer.

This abstracts the commands required for development.

For example:

If a developer/tester needs to start the webserver, then should **NOT* * care if you are using vagrant or php built-in webserver.
They should just run the same command (eg. make dev.server). This way, when updating the architecture, the same commands 
 can be run, even if they are doing something slightly different or more than in an earlier version.

## Usage

1. Create a `Makefile` in the root of your project.

2. Added a `LOCATION` parameter to the top of the `Makefile`

```
LOCATION=.
```

If you have brought in this Helper Library with `composer`, then you need to update the location of the include files.

In your main Makefile update the location parameter:

```
LOCATION=vendor/eddiejaoude/dev-helper-cmds
```

*Note: must **NOT** end in a `/`*

3. Now include the *commands* you want to use or include all by adding the following to your `Makefile`

```
include $(LOCATION)/include.all
```

4. Then you are done.

Below our the built-in commands. 
 
### Overriding commands

You can override these by adding to your Makefile that contains all the includes.

```
# ---
# Below is example overwriting commands
# Note: you will get warnings
# ---

symfony.test.spec:
	bin/phpspec run  --config test/phpspec.yml

symfony.test.bdd:
	bin/behat --config test/behat.yml 
```

### Combining commands to make new ones

It is also possible to combine exist or new commands with a new command:

```
new.command: old.cmd1 old.cmd2
    echo NEW CMD
```

---

### Built-in commands

#### Git commands

* `make git.status`

#### Composer commands

* `make composer.download`
* `make composer.install`
    * dependency on `composer.download`
* `make composer.update`
    * dependency on `composer.download`

#### Symfony

##### Running tests in parallel using Robo

* `make symfony.test.run`
    * dependency on Robo

##### Running Behat tests

* `make symfony.test.bdd`
    * dependency on Behat & SymfonyBehat bundle
    
##### Running PHPSpec

* `make symfony.test.spec`
    * dependency on PHPSpec
    
##### Running PHPUnit

* `symfony.test.unit`

