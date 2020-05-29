[![Build Status](https://travis-ci.com/wikimedia/fresh.svg?branch=master)](https://travis-ci.com/wikimedia/fresh)

# 🌱  Fresh environment

A **Fresh** environment is a fast and ready-to-use Docker container with
various developer tools pre-installed. Including Node.js, and headless
browsers. It aims to help to run npm packages on your machine,
_without_ putting your personal data at risk!

## Quick start

Run the following from a terminal:

```sh
bash -c 'curl -fsS https://gerrit.wikimedia.org/g/fresh/+/20.05.1/bin/fresh-node10?format=TEXT \
| base64 --decode > /usr/local/bin/fresh-node \
&& echo "8eeb4fb81974f9f0189471d878658c636af773e731261e0f9394208abfd9e98e  /usr/local/bin/fresh-node" | shasum -c \
&& chmod +x /usr/local/bin/fresh-node \
&& echo -e "\n\xf0\x9f\x8c\xb1\x20Fresh\x20is\x20ready\x21\n"||(echo -e "\xe2\x9d\x8c";false)'
```

This will save [fresh-node](/bin/fresh-node10) to the `/usr/local/bin/` directory, verify its integrity, and make it executable.

Programs in this directory automatically become commands you can run from your terminal.

### What's inside

* **Node.js** 10 with npm 6
* **Firefox**
* **Chromium**
* `chromedriver`, `ffmpeg`, and `xvfb` (for browser tests)
* JSDuck
* Debian Linux 9 Stretch

### Prerequisites

You'll need to have Docker installed. See [Docker CE for Linux](https://docs.docker.com/install/#server), [Docker for Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac), or [Docker for Windows](https://docs.docker.com/docker-for-windows/install/).

### Issue tracker

Report bugs or feature requests to [Wikimedia Phabricator](https://phabricator.wikimedia.org/tag/fresh/).

### Integrity

Verify the integrity of your installation at any time, by running `shasum -a 256 /usr/local/bin/fresh-node` and compare the [SHA-256 checksum](https://en.wikipedia.org/wiki/SHA-256) against the below.

| Checksum for Fresh 20.05.1 |
|-------|
| `8eeb4fb81974f9f0189471d878658c636af773e731261e0f9394208abfd9e98e` |

To update or repair your copy, simply [re-install Fresh](#quick-start).

## Usage

With Fresh installed, navigate your terminal to a project directory in which
you might need to run commands like `npm install` or `npm test`.
Before you run such commands, use `fresh-node` to enter a Fresh environment.

```
you@precious.local:~$ cd myproject/
you@precious.local:myproject$ fresh-node

# fresh: …
# image: docker-registry.wikimedia.org/…/node10-test-browser:…
# software: Debian Linux 9 Stretch
#           Node.js 10 (npm 6)
#           Chromium …
#           Mozilla Firefox …
#           JSDuck (Ruby 2.3)
# mount: /myproject ➟ /Users/you/myproject (read-write)

🌱  Fresh!

nobody@76010858c836:/myproject$
```

You can now execute commands such as `npm install`, `npm test`, and
other `npm run` commands.

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
of a second. This is made possible by Docker and its `docker run` command.
It doesn't need to copy or clone anything. Instead, it references the
downloaded Docker image as bottom layer (read-only) in an empty container,
with a new (initially empty) read-write layer on top. This uses the
"copy-on-write" principle, powered by [UnionFS](https://en.wikipedia.org/wiki/UnionFS).

### Isolation

You can start as many independent Fresh environments as you want,
without taking up a lot of disk space, and without different sessions
affecting each other.

Only the directory from which you launch Fresh, is made visible to the container.
The rest of your personal hard drive is not mounted, and most networking
capabilities are also disabled (except toward the Internet). Specifically,
local servers and networked devices on your home network are not easily
reachable.

Any changes made elsewhere in the container, are lost once you exit Fresh.

### Why?

When you open an application or execute a program from the terminal,
that program can do **anything** that you can do. This should scare you.

See also _[The worst that could happen](https://timotijhof.net/posts/2019/protect-yourself-from-npm/)_.

To create your own Docker base image, see [Tutorial.md](./Tutorial.md).
