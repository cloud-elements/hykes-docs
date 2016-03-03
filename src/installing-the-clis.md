# Installing the CLIs

This page will show you how to install the Hykes CLIs on your local system. These CLIs make up the
core foundation of the Hykes solution which, combined together, will allow you to get a Cloud
Elements cloud up and running quickly and easily. The guide currently assumes you are running the
most recent version of OS X.

When you finish, you will have the Hykes CLIs installed on your local system and can then proceed
to the next page of the guide.

## Homebrew <sub><sup>(Estimated time: 0 to 30 minutes)</sup></sub>
Hykes makes use of Homebrew taps. Homebrew is the missing package manager for OS X. Leveraging the
Hykes Homebrew tap will allow you to install the Hykes CLIs with minimal effort. If you do not
already have it installed, proceed to the
[Homebrew project documentation](https://github.com/Homebrew/homebrew/blob/master/share/doc/homebrew/Installation.md)
and follow the installation instructions, ensuring that you also satisfy the requirements.

## Tapping <sub><sup>(Estimated time: 1 to 5 minutes)</sup></sub>
As mentioned, Hykes makes use of Homebrew taps to ease installation of the Hykes CLIs. What wasn't
mentioned is that this is an
[open source project](https://github.com/cloud-elements/homebrew-hykes), which you can freely
inspect, follow along with, or contribute to. To tap, simply:

```bash
$ brew tap cloud-elements/hykes
```

## Installing <sub><sup>(Estimated time: 1 to 5 minutes)</sup></sub>

Installing `hykes-blueprint`:

```bash
$ brew install hykes-blueprint
```

Install `hykes-provision`:

```bash
$ brew install hykes-provision
```

Install `hykes-engine`:

```bash
$ brew install hykes-engine
```
