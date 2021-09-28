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
  * Updated Mozila Firefox from 68.11.0esr to 68.12.0esr.

### Fixed

* Containers now exit automatically when closing a terminal tab (Timo Tijhof)

21.01.1 / 2021-01-27
==================

### Added

* Add `--env-sauce` flag to support forwarding SAUCE_ environment variables (Timo Tijhof)
* Add support for Podman, an alternative container execution tool to Docker (Timo Tijhof & Kunal Mehta) [T259974](https://phabricator.wikimedia.org/T259974)

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
