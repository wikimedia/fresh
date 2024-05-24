# Create your own Fresh environment

## Dockerfile

The base image is generated from these Docker files:

* [node/Dockerfile](https://github.com/wikimedia/integration-config/blob/0fb154c75de0c4fbc5b0529e40c8785ff4aa309f/dockerfiles/node20/Dockerfile.template),
* [node-test/Dockerfile](https://github.com/wikimedia/integration-config/blob/0fb154c75de0c4fbc5b0529e40c8785ff4aa309f/dockerfiles/node20-test/Dockerfile.template), and
* [node-test-browser/Dockerfile](https://github.com/wikimedia/integration-config/blob/0fb154c75de0c4fbc5b0529e40c8785ff4aa309f/dockerfiles/node20-test-browser/Dockerfile.template).

## Bash script

The bash script that quickly launches a temporary container can be found
at [bin/fresh-node](./bin/fresh-node20).

The script is documented inline, but I'll take apart the most
import line here as well, the `docker run` command.

```
docker run --rm --interactive --tty \
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

* `--mount`: This is used to expose the current working directory from
  the host machine, to the container. Typically a Git project with source
  code. See [Docker Docs: mount](https://docs.docker.com/storage/bind-mounts/)
  for more information.

* `--entrypoint`: This decides which shell command to run inside the
  container. In our case `/bin/sh`. The parameters to this command are
  specified after the base image name. The full command to be executed is:
  `/bin/sh -c "cd $mountdest/;$welcomecmd;bash"`. This opens the current
  directory in the container, prints the welcome message, and starts Bash.

The Wikimedia base images run as the unprivileged `nobody` user inside the
container. This user has no writable home directory. However, we set
various environment variables to accomodate CLI utilities that assume
directories such as `$HOME` to exist and be writable ([T365871](https://phabricator.wikimedia.org/T365871)).
