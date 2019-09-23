# 🌱  Fresh environment

A **Fresh** environment is a fast and ready-to-use Docker container with
various developer tools pre-installed. Including Node.js, and headless
browsers. It aims to help to run npm packages on your machine,
_without_ putting your personal data at risk!

## Quick start

Run the following from a terminal:

```sh
curl -s https://raw.githubusercontent.com/wikimedia/fresh/19.09.1/bin/fresh-node10 \
> /usr/local/bin/fresh-node \
&& chmod +x /usr/local/bin/fresh-node \
&& echo -e '\n\xf0\x9f\x8c\xb1\x20Fresh\x2019.09.1\x20is\x20now\x20ready\x21\n'
```

This will save [fresh-node](/bin/fresh-node10) to `/usr/local/bin/`, and marks the file as executable.

Programs in this directory automatically become commands you can run from your terminal.

### Integrity

Verify the integrity of your installation by computing the SHA-512 checksum of the installed script. For example, by running `shasum -a 512 /usr/local/bin/fresh-node`. Then, comparing it to the table below. 

| Checksum for Fresh 19.09.1
|--
| `8d53fda6330314…5587a63ed4744f`

Alternatively, run the below script and confirm that it outputs `fresh-node: OK`.

```sh
integrity=8d53fda633031496507aab6edda792d3fe40e8a54d07bc37d040c0486c65f1f7d372b40d89e6532da5a36725cf6f5e78dd51cc2872423de5a5587a63ed4744ff;
echo "$integrity  /usr/local/bin/fresh-node" | shasum -c || (echo -e "\xe2\x9d\x8c"; exit 1)
```

### What's inside

* **Node.js** 10 with npm 6
* **Firefox**
* **Chromium**
* `chromedriver`, `ffmpeg`, and `xvfb` (for browser tests)
* JSDuck
* Debian Linux 9 Stretch

### Prerequisites

You'll need to have Docker installed. See [Docker CE for Linux](https://docs.docker.com/install/#server), [Docker for Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac), or [Docker for Windows](https://docs.docker.com/docker-for-windows/install/).

## Usage

With Fresh installed, navigate your terminal to a project directory in which
you might need to run commands like `npm install` or `npm test`.
Before you run such commands, use `fresh-node` to enter a Fresh environment.

```
you@precious.local:~$ cd myproject/
you@precious.local:myproject$ fresh-node

# fresh: 19.09.1
# image: docker-registry.wikimedia.org/…/node10-test-browser:…
# software: Debian Linux 9 Stretch
#           Node.js 10 (npm 6)
#           Chromium …
#           Mozilla Firefox …
#           JSDuck 5 (Ruby 2.3)
# mount: /myproject ➟ /Users/you/myproject (read-write)

🌱  Fresh!

nobody@76010858c836:/myproject$
```

You can now execute commands such as `npm install`, `npm test`, and
other `npm run` commands.

### Fish shell

If using Fish shell, you can use [bass](https://github.com/edc/bass) to execute `fresh-node` with `bass fresh-node`.

## How does it work

The first time you start a Fresh environment, Docker will download the
container image layers from `docker-registry.wikimedia.org`. This may take
a few minutes.

The fresh-node command uses the [`node10-test-browser` image](./Tutorial.md#start-of-content),
which is the same exact image used by Jenkins CI at Wikimedia Foundation.
This means you can trust that if it works in Fresh, it'll work in CI.
And vice-versa, you can use Fresh to locally reproduce test failures.

### Fast

Fresh is fast. Creating and launching a new container takes only a fraction
of as second. This is made possible by Docker and its `docker run` command.
It doesn't need to copy or clone anything. Instead, it references the
downloaded Docker image as bottom layer (read-only) in an empty container,
with a new (initially empty) read-write layer on top. This uses the
"copy-on-write" principle, powered by [UnionFS](https://en.wikipedia.org/wiki/UnionFS).

### Isolation

You can start as many independent Fresh environments as you want,
without taking up a lot of disk space, and without different sessions
affecting each other.

Only the directory from which you launch Fresh, is made visbile to the container.
The rest of your personal hard drive is not mounted, and most networking
capabilities are also disabled (except toward the Internet). Specifically,
local servers and networked devices on your home network are not easily
reachable.

Any changes made elsewhere in the container, are lost once you exit Fresh.

## Why?

When you open an application or execute a program from the terminal,
that program can do **anything** that you can do. This should scare you.

See also _[The worst that could happen](https://medium.com/@timotijhof/how-to-protect-yourself-from-vulnerable-npm-packages-c03f85249651)_.

To create your own Docker base image, see [Tutorial.md](./Tutorial.md).
