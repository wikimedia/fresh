# Create your own Fresh environment

## Dockerfile

The base image is generated from these Docker files:

* [node/Dockerfile](https://github.com/wikimedia/integration-config/blob/2a3f3ff2b41bbdfaf0044dbed23a2272353dcdee/dockerfiles/node12/Dockerfile.template#L1),
* [node-test/Dockerfile](https://github.com/wikimedia/integration-config/blob/2a3f3ff2b41bbdfaf0044dbed23a2272353dcdee/dockerfiles/node12-test/Dockerfile.template#L1), and
* [node-test-browser/Dockerfile](https://github.com/wikimedia/integration-config/blob/2a3f3ff2b41bbdfaf0044dbed23a2272353dcdee/dockerfiles/node12-test-browser/Dockerfile.template#L1).

## Bash script

The bash script that quickly launches a temporary container can be found
at [bin/fresh-node](./bin/fresh-node#L3).

The script is documented inline, but I'll take apart the most
import line here as well, the `docker run` command.

```
docker run --rm --interactive --tty -e 'HOME=/tmp' \
	--mount type=bind,source="$mountsrc",target="$mountdest",consistency=delegated \
	--mount type=bind,source="$mountsrc"/.git,target="$mountdest"/.git,readonly,consistency=cached \
	--entrypoint /bin/sh \
	"$imagename:$imageversion" \
	-c "cd $mountdest/;$welcomecmd;bash"
```

At a high level, the `docker run` command does three things:

* Creates a new container, based on a specified base image name+version.
* Start the container.
* Run a shell command in the container.

The first positional argument, `"$imagename:$imageversion"`, is the base
image we download at first run from wikimedia.org. This has Node.js, Firefox,
etc. installed.

The various options before it decide how the container is configured:

* `--rm`: This marks the container as temporary, to be automatically
  deleted after you exit the container. Without this, the container
  could be re-used by other docker commands.

* `--interactive` `--tty`: These make it possible for you to type into the
  container's bash prompt.

* `-e 'HOME=/tmp'`: The Wikimedia base images run as the unprivileged
  `nobody` user inside the container, which has no home directory.
  This is for compatibility with various CLI utilities that assume
  the `$HOME` directory to exist.

* `--mount`: This is used to expose the current working directory from
  the host machine, to the container. Typically a Git project with source
  code. See [Docker Docs: mount](https://docs.docker.com/storage/bind-mounts/)
  for more information.

* `--entrypoint`: This decides which shell command to run inside the
  container. In our case `/bin/sh`. The parameters to this command are
  specified after the base image name. The full command to be executed is:
  `/bin/sh -c "cd $mountdest/;$welcomecmd;bash"`. This opens the current
  directory in the container, prints the welcome message, and starts Bash.

