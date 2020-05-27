---
layout: wiki_archive
---
## Docker Builder Pattern

For compiled languages, [/docker/](../docker.md) workflow often uses the **builder
pattern**.

### What is it?

High-level:

  - Derive their Dockerfiles from an image, then, add source
  - do a build during `docker build`
  - create a second docker container with just binaries using a second
    Dockerfile
  - push it to the Docker Hub

> With a statically compiled language like Golang people tended to
> derive their Dockerfiles from the Golang "SDK" image, add source, do a
> build then push it to the Docker Hub. Unfortunately the size of the
> resulting image was quite large - at least 670mb.

\>

> A workaround which is informally called the builder pattern involves
> using two Docker images - one to perform a build and another to ship
> the results of the first build without the penalty of the build-chain
> and tooling in the first image.

\>

> <http://blog.alexellis.io/mutli-stage-docker-builds/>

  - Advantage: build environment is bundled with binaries, making
    development easier
  - Disadvantage: images are larger because they include source files.
  - Workaround: 2 images. One for dev, one for deploy.

### The Future

In Future, it will be possible to do
[multi-stage](http://blog.alexellis.io/mutli-stage-docker-builds/)
builds in Docker instead, removing the need for multiple images.

### Resources

  - <https://medium.com/@alexeiled/docker-pattern-the-build-container-b0d0e86ad601>
  - <http://blog.alexellis.io/mutli-stage-docker-builds/>
  - <http://blog.terranillius.com/post/docker_builder_pattern/>
