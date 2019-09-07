# Docker images for openblack

This repository contains `Dockerfile`s for generating various docker images used by openblack's CI.
This was done to address the problem of having docker images available, without the need to build them by each CI job, taking lots of time -- usually of about total 30 minutes spent in given job, more than 20 was used to build a throwaway docker image.


# How it works

The project has an organisation enabled for it on docker hub: https://hub.docker.com/r/openblack/openblack and this repository is set to have automated builds for it.
Each time a commit is done here modifying one of the `Dockerfile`s, a build will be automatically triggered resulting in an updated docker images for use in CI. Downloading such prebuilt image is much faster than creating them on the go and addresses the problem of reproducability.

## Packages
Some images don't come with all the required packages -- they are provided with `hunter` package manager for CMake instead.

## How it is set up

To set it up, a `Dockerfile` for each of the supported configurations has to be created. To allow for easy separation, each of the the files is stored in a separate directory and gets an entry on docker hub. While original files were templated, there is no support for templating on docker hub and they have to written out explicitly.
See the image below for the docker hub configuration:
![Docker hub screenshot](https://raw.githubusercontent.com/openblack/openblack-docker/master/docs/openblack-docker-hub-setup.png)

## Adding an image

To add an image, start by defining what purpose you want it to serve and present it to team. When ack'd, start locally by crafting some base functionality of a given image: install at least `cmake`, `git`, C++ compiler and enter the container to clone the project and install required packages until you are satisified with them. Wrap it up in `RUN` command that installs them automatically. Ensure proper operation of the CI script from the main repo, when launched in your new docker image. Communicate the name of the image to the team, so it can get its entry on docker hub. Submit `Dockerfile` for review.

### Tips

* Package managers like to keep the downloaded copy cached. Remember to clean it up, e.g. `dnf clean all`
* Package managers target users of full-blown installations an might have optional, unnecessary from the point of view of CI, dependencies. See if you can disable them, e.g. `apt-get install -y --no-install-recommends`

## Build frequency

The images shouldn't change too often, but can be manually triggered via docker hub web UI. There will be a build triggered after each commit to this repository, though keep in mind it is configured to use cache. 

## Docker hub vs `push`ing images to registry

One important difference between docker hub and `push`ing a locally-built image (e.g. on Travis CI) is hub's ability to automatically trigger rebuilds upon changes of base images (`Dockerfile`'s `FROM`). This should happen roughly once monthly for Ubuntu-based images and once per two weeks for Fedora-based images, as evident by their hub history.
