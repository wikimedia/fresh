# Create your own Fresh environment

## Quick start

* The base image is generated from:
  * [wikimedia/integration-config:node10/Dockerfile](https://github.com/wikimedia/integration-config/blob/de60ab21ed/dockerfiles/node10/Dockerfile.template#L1),
  * [wikimedia/integration-config:node10-test/Dockerfile](https://github.com/wikimedia/integration-config/blob/de60ab21ed/dockerfiles/node10-test/Dockerfile.template#L1), and
  * [wikimedia/integration-config:node10-test-browser/Dockerfile](https://github.com/wikimedia/integration-config/blob/de60ab21ed/dockerfiles/node10-test-browser/Dockerfile.template#L1).
* The bash script to quickly launch a temporary container
  and mount the current directory:
  * [bin/fresh-node10](./bin/fresh-node10#L3)

