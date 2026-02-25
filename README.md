# Cutehax0r Apt Repository

Visible at: https://cutehax0r.github.io/apt-repo/

## How do I install these packages?

Add the repository key
```sh
curl -fsSL https://cutehax0r.github.io/apt-repo/key.asc | sudo apt-key add -
```

Then setup the repository on your local system

```sh
curl -fsSL https://cutehax0r.github.io/apt-repo/key.asc | sudo tee /etc/apt/trusted.gpg.d/cutehax0r.asc

echo "deb [arch=amd64] https://cutehax0r.github.io/apt-repo stable main" | sudo tee /etc/apt/sources.list.d/proji.list
```

then

```sh
sudo apt update
sudo apt install <package>
```

or install a specific version with

```sh
sudo apt install <package>=<version>
```

## Documentation

`man apt` or check [Apt's documentation](https://wiki.debian.org/Apt).

## Requirements

If you're developing this on macOS or a non-Debian Linux you're going to run into issues with the
apt-repository build process. Use a [podman](https://podman-desktop.io/) shell for the APT steps:
`apt-ftparchive` step. Dpkg can be install via homebrew or run via podman's container.

```sh
podman machine start
podman pull debian:stable
podman run --rm -it -v /Users/you/apt-repo:/repo  -w /repo debian:stable /bin/bash
```

# Wishlist

  * Basic functionality

    * Push this repo up to github.

    * Make this exposed on github pages.

    * Test that we can clone add the repo to debian and install via podman

    * Build a workflow for proj that will checkout the repo, add the debs, rebuild and sign releases

  * Build a makefile to help with maintenance.

    * `release-all` - builds latest version of all taps

    * `release FOO` - updates a particular project

    * `unrelease FOO` - deletes the most recent release of `foo` and makes the previous version current

    * `unrelease FOO VERSION` - deletes a specific version of foo (rolling back head if required

    * `lint` - checks for syntax issues.

    * `test` - some kind of docker/container/emu "test that it installs on a clean system" test

    * `test FOO` - test a specific formula only

    * `test FOO version` - test a specific formula version only

    * `deploy` - Take all the local changes and make them public `git push`
