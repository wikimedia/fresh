24.05.1
==================

### Added

* Provide fresh-node22. (James D. Forrester)

  Based on Debian 11 Bullseye with Node.js 22, npm 10, Firefox 115,
  and Chromium 120.

* fresh-npm: initial commit. (Timo Tijhof)

  This is a new opt-in security feature available via `fresh-install --secure-npm`.
  This shadows the npm command in your shell and avoids accidentally running
  potentially insecure scripts outside Fresh.
  Other npm commands are unaffected. It can be bypassed as-needed by
  specifying the full path to npm, which can also be found at the end
  of the fresh-npm help message.

### Fixed

* Fix instance name to avoid spaces or other unsupported characters. (Marius Hoch)

### Changed

* fresh-install: Promote fresh-node20 to be the default. (Timo Tijhof)
* fresh-node18: Update image to docker-registry.wikimedia.org/releng/node18-test-browser:18.20.2-s1. (James Forrester) [T362908](https://phabricator.wikimedia.org/T362908)
  * Update Node.js from 18.17.0 to 18.20.2.
  * Update npm from 9 to 10.
  * Update Firefox from 102 to 115.
  * Update Chromium from 115 to 120.
* fresh-node20: Update image to docker-registry.wikimedia.org/releng/node18-test-browser:20.12.2-s1. (James D. Forrester)
  * Upgrade Node.js from 20.5.0 to 20.12.2.
  * Update npm from 9 to 10.
  * Update Firefox from 102 to 115.
  * Update Chromium from 115 to 120.

### Removed

* fresh-node14: Remove command and uninstall during upgrade. (James D. Forrester)
* fresh-node18,20,22: Move `HOME=/tmp` to upstream and remove override. (Timo Tijhof) [T365871](https://phabricator.wikimedia.org/T365871)

23.08.1
==================

### Added

* Set podman flag when docker is really podman. (Antoine Musso)
* Set `--user` and `--userns` for Podman on Mac as well. (Timo Tijhof)
* Add command `fresh-node18` which comes with Node.js 18 and npm 9. (James Forrester) [T337647](https://phabricator.wikimedia.org/T337647)
* Add command `fresh-node20` which comes with Node.js 20 and npm 9.

### Changed

* fresh-install: Promote fresh-node18 to be the default. (Timo Tijhof)
* fresh-node16,18,20: Hide "unrequested emulation" warning on Apple ARM. (Timo Tijhof)
* fresh-node16: Update image to docker-registry.wikimedia.org/releng/node16-test-browser:0.2.1
  * Update npm from 7.21.0 to 8.19.3.
  * Update Chromium from 112 to 115.

### Removed

* fresh-node12: Remove command and uninstall during upgrade.

23.05.1
==================

### Changed

* Add `<command>` positional argument to all fresh-node scripts. For example: `fresh-node -- npm test` (Gergő Tisza) [T253924](https://phabricator.wikimedia.org/T253924)
* fresh-node16: New and shorter welcome message. (Timo Tijhof)
* fresh-node16: Update image to docker-registry.wikimedia.org/releng/node16-test-browser:0.2.0
  * Update Firefox from 102.8.0esr to 102.10.0esr.
  * Update Chromium from 110 to 112.

22.11.2
==================

### Changed

* fresh-node16: Update image to docker-registry.wikimedia.org/releng/node16-test-browser:0.1.0
  * Update Node.js from 16.16.0 to 16.19.1.
  * Update Firefox from 91.11.0esr to 102.8.0esr.
  * Update Chromium from 103 to 110.

22.11.1
==================

### Added

* fresh-node16: Add `--env-bs` option to forward BrowserStack environment variables. (Timo Tijhof)
* fresh-node16: Add `--env=PREFIX` option to forward any environment variables. (Timo Tijhof)

### Changed

* fresh-install: Improve error message for ZSH on macOS 10.15+. (Peter Hedenskog) [T310490](https://phabricator.wikimedia.org/T310490)

22.09.1
==================

### Added

* Add command `fresh-node16` which comes with Node.js 16 and npm 7 (James Forrester) [T314347](https://phabricator.wikimedia.org/T314347)
* fresh-node16: Compared to fresh-node15, this effectively includes:
  * Update Chromium from 97 to 103.
  * Update Mozilla Firefox from 91.5.0esr to 91.11.0esr.
* fresh-install: Promote fresh-node16 to be the default. (Timo Tijhof)

22.05.1
==================

### Added

* fresh-install: Support installing to `~/.local/bin` for Linux. (Antoine Musso) [T282879](https://phabricator.wikimedia.org/T282879)

### Changed

* fresh-install: Promote fresh-node14 to be the default. [T307385](https://phabricator.wikimedia.org/T307385)

## Removed

* fresh-node10: Remove command and uninstall during upgrade. (Timo Tijhof)

22.01.1
==================

### Added

* fresh-node12: Add `npx` command.
* fresh-node14: Add `npx` command.

### Changed

* fresh-node12: Bump image to `releng/node12-test-browser:0.0.3-s3`.
  * Update npm from 7.5.2 to 7.21.0.
  * Update Chromium from 90 to 97.
  * Update Mozilla Firefox from 78esr to 91esr.
* fresh-node14: Bump image to `releng/node14-test-browser:0.0.2-s4`.
  * Update npm from 7.5.2 to 7.21.0.
  * Update Chromium from 90 to 97.
  * Update Mozilla Firefox from 78esr to 91esr.

21.09.1
==================

### Added

* Add command `fresh-node12` which comes with:
  * Node.js 12 and npm 7.
  * Chromium 90, Mozilla Firefox 78, Debian Linux 11 Bullseye.
* Add command `fresh-node14` which comes with:
  * Node.js 14 and npm 7.
  * Chromium 90, Mozilla Firefox 78, Debian Linux 11 Bullseye.

21.04.1 / 2021-04-29
==================

### Changed

* Bump Docker image to `node10-test-browser:0.6.3-s2`.
  * Updated Chromium from 71 to 73.
  * Updated Mozilla Firefox from 68.11.0esr to 68.12.0esr.

### Fixed

* Containers now exit automatically when closing a terminal tab. (Timo Tijhof)

21.01.1 / 2021-01-27
==================

### Added

* Add `--env-sauce` flag to support forwarding SAUCE_ environment variables. (Timo Tijhof)
* Add support for Podman, an alternative container execution tool to Docker. (Timo Tijhof & Kunal Mehta) [T259974](https://phabricator.wikimedia.org/T259974)

### Changed

* The `-env` option will emit a warning if no MW environment variables are found. (Timo Tijhof)

20.08.1 / 2020-08-27
==================

### Changed

* Bump Docker image to `node10-test-browser:0.6.2`. (Antoine Musso)
  * Updated npm from 6.5.0 to 6.14.5.
  * Updated Mozilla Firefox from 68.3.0esr to 68.11.0esr.

### Fixed

* Make file writes work on SELinux by disabling its "security labels" from Docker. (Marius Hoch)

20.05.1 / 2020-05-28
==================

### Added

* The `-env` option now also reads and forwards variables from a `.env`
  file in the current directory. (Kosta Harlan) [#16](https://github.com/wikimedia/fresh/issues/16)

### Changed

* On Linux, the container now runs as your host user/group rather than as the
  unknown 1001 uid. This means the mounted directory is as read-writable
  within the container as it is outside, matching how Fresh works with
  Docker for Mac. (Stephen Niedzielski) [#11](https://github.com/wikimedia/fresh/issues/11)

### Fixed

* Fix launch in host environments without `tput` installed. (Timo Tijhof) [T251309](https://phabricator.wikimedia.org/T251309)
* Fix launch in terminals that only support bold/greyscale markup. (Timo Tijhof) [T251309](https://phabricator.wikimedia.org/T251309)
* Fix mounted directory being writable on Linux. (Kosta Harlan) [#11](https://github.com/wikimedia/fresh/issues/11)

20.02.1 / 2020-02-08
==================

### Changed

* Bump Docker image to `node10-test-browser:0.6.1`. (James Forrester)
  * Updated Mozilla Firefox from 60.8.0 to 68.3.0esr.

### Fixed

* Remove non-existent "-git" option from help text. (Kosta Harlan)

19.10.1 / 2019-10-01
==================

### Changed

* Bump Docker image to `node10-test-browser:0.6.0-s1`. (Timo Tijhof)
  * Updated Mozilla Firefox from 60.7.0 to 60.8.0.

### Fixed

* Use system default `grep`, avoid local alias. (Kosta Harlan) [#7](https://github.com/wikimedia/fresh/pull/7), [#8](https://github.com/wikimedia/fresh/pull/8)
* Fix mount error when launched in directory without a ".git". (Scott B) [#3](https://github.com/wikimedia/fresh/issues/3), [#9](https://github.com/wikimedia/fresh/pull/9)

19.09.1 / 2019-09-12
==================

* First stable release. (Timo Tijhof)
