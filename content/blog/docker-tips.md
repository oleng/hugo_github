---
title: "Docker tips"
date: 2020-01-04T09:05:44Z
tags: [ "development", "containers" ]
draft: false
---

Some useful tips for docker:

1. Making shortcuts for useful commands (with flags) to free up space is one time effort compared to remembering which command Docker provides. Use `alias` on macOS and put them in `~/.bash_profile` so they're loaded in your terminal (I use `~/.bashrc` for aliases holder, which needs to be sourced unlike `.bash_profile`, see my [.dev/dotfiles](https://github.com/oleng/.dev/tree/master/dotfiles) repo for more info). Alias is auto completed in bash.

```bash

# remove just dangling images
alias docker-dangling-images="docker rmi $(docker images --filter dangling=true)"

# remove every stopped containers
alias docker-stopped-containers="docker rm $(docker ps -a -q -f status=exited)"

# remove every stopped containers, also
# all networks not used by at least one container,
# all dangling images & dangling build cache
alias dockerprune="docker system prune"

```

2. Useful to modify Docker Hyperkit VM's transparent_hugepages setting in case of redis complaining (macOS Mojave 10.14.x)

> `WARNING you have Transparent Huge Pages (THP) support enabled in your kernel.`

see
: https://github.com/docker-library/redis/issues/55#issuecomment-368346882
: https://stackoverflow.com/questions/39739560/how-to-access-the-vm-created-by-dockers-hyperkit)
: https://kerneltalks.com/services/what-is-huge-pages-in-linux/

```bash

screen ~/Library/Containers/com.docker.docker/Data/vms/0/tty

echo never > /sys/kernel/mm/transparent_hugepage/enabled
echo never > /sys/kernel/mm/transparent_hugepage/defrag

# exit: Ctrl-A-K then y

```
	
3. Docker build (or docker-compose build) tips:

- Use multi stage build for faster build
- Clean up build artifacts & caches on the same command line layer, each `RUN` line adds an immutable layer which affects final image file size.

4. Docker-compose:

- use `$$` (double-dollar sign) when using an existing environment variable to escape/prevent docker-compose interpolating a value.
Example for path defined with `$PGDATA` environment variable in official postgresql image:

```yaml

db:
	image: postgres:9.6
	volumes:
		- ./postgres:$$PGDATA

```

`"${VAR}"` (with curly bracket inside double quotation mark) or `"$VAR"` syntax works for shell variable, but docker-compose (depending on which file format version) expecting `"${VAR}"` value from `.env` file (exact name `.env` needed, otherwise ignored) when evaluating `docker-compose.yml`, and [issues a warning](https://github.com/docker/compose/blob/d412a1e47fcbf58674a54247f021a2d63627018d/compose/config/environment.py#L48) if `.env` file is not supplied/found:

```
WARNING: The PGDATA variable is not set. Defaulting to a blank string.
```
Read more in [the docs](https://docs.docker.com/compose/compose-file/#variable-substitution), and be sure to check on which corresponding version you're using.


