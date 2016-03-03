# Creating a Blueprint

This page will show you how to use the stubbing feature of `hykes-blueprint`, which you can
then configure for use with your own cloud.

When you finish, you will have a basic Hykes blueprint created that can then be used to build one
or more concrete clouds.

## Stubbing <sub><sup>(Estimated time: 1 to 5 minutes)</sup></sub>
`hykes-blueprint` comes with a number of useful commands for interacting with Hykes blueprints.
One collection of commands includes one-liner easy encryption and decryption commands, so that you
could encrypt the entirety of a blueprint at rest so that the contents could be hosted on a private
Git remote, such as GitHub. Another useful command is the `stub` command:

```bash
$ hykes-blueprint stub /path/to/blueprint
$ cd /path/to/blueprint
```

This command pulls the current [hykes-spec](https://github.com/cloud-elements/hykes-spec) into the
specified directory. You can then configure the blueprint to your own needs.

## Configuring <sub><sup>(Estimated time: 10 to 120 minutes)</sup></sub>
With the stubbed blueprint now on our local filesystem, we make make tweaks to it for our own cloud.

### Inventory:
The [hykes.ini](https://github.com/cloud-elements/hykes-spec/blob/master/hykes.ini) file serves as
a simple description of the quantity of servers which make up each role in your cloud.

### Configuration system config:
The [hykes.yml](https://github.com/cloud-elements/hykes-spec/blob/master/hykes.yml) file exposes a
simple lifecycle which has global and per role phases. Each has:

* Pre/post hook blocks, in which any Bash commands can be specified and will be executed when
building
* Build variable block, in which variables you define will be made available during the build
process
* Environment variable block, in which variables you define will be made available on all servers
belonging to that role as environment variables that persist through restarts

### Configuration system filesystem:
In addition to the configuration system config, root level directories that match up to one of the
lifecycle phases will have their contents copied over to the matching servers. Combined together,
this makes for an extremely easy and flexible way to make customizations to your own cloud.
