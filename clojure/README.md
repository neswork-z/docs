<!--

********************************************************************************

WARNING:

    DO NOT EDIT "clojure/README.md"

    IT IS AUTO-GENERATED

    (from the other files in "clojure/" combined with a set of templates)

********************************************************************************

-->

# Supported tags and respective `Dockerfile` links

-	[`openjdk-8-lein`, `openjdk-8-lein-2.9.1`, `lein-2.9.1`, `lein`, `latest`](https://github.com/Quantisan/docker-clojure/blob/f4257cfa677af38c2f8a9cd0455747c9bee835ca/target/openjdk-8/debian/lein/Dockerfile)
-	[`openjdk-8-boot`, `openjdk-8-boot-2.8.2`, `boot-2.8.2`, `boot`](https://github.com/Quantisan/docker-clojure/blob/f4257cfa677af38c2f8a9cd0455747c9bee835ca/target/openjdk-8/debian/boot/Dockerfile)
-	[`openjdk-8-tools-deps`, `openjdk-8-tools-deps-1.10.0.442`, `tools-deps-1.10.0.442`, `tools-deps`](https://github.com/Quantisan/docker-clojure/blob/f4257cfa677af38c2f8a9cd0455747c9bee835ca/target/openjdk-8/debian/tools-deps/Dockerfile)
-	[`openjdk-11-lein`, `openjdk-11-lein-2.9.1`](https://github.com/Quantisan/docker-clojure/blob/f4257cfa677af38c2f8a9cd0455747c9bee835ca/target/openjdk-11/debian/lein/Dockerfile)
-	[`openjdk-11-boot`, `openjdk-11-boot-2.8.2`](https://github.com/Quantisan/docker-clojure/blob/f4257cfa677af38c2f8a9cd0455747c9bee835ca/target/openjdk-11/debian/boot/Dockerfile)
-	[`openjdk-11-tools-deps`, `openjdk-11-tools-deps-1.10.0.442`](https://github.com/Quantisan/docker-clojure/blob/f4257cfa677af38c2f8a9cd0455747c9bee835ca/target/openjdk-11/debian/tools-deps/Dockerfile)

[![arm64v8/clojure build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/arm64v8/job/clojure.svg?label=arm64v8/clojure%20%20build%20job)](https://doi-janky.infosiftr.net/job/multiarch/job/arm64v8/job/clojure/)

# Quick reference

-	**Where to get help**:  
	[the Docker Community Forums](https://forums.docker.com/), [the Docker Community Slack](https://blog.docker.com/2016/11/introducing-docker-community-directory-docker-community-slack/), or [Stack Overflow](https://stackoverflow.com/search?tab=newest&q=docker)

-	**Where to file issues**:  
	[https://github.com/Quantisan/docker-clojure/issues](https://github.com/Quantisan/docker-clojure/issues)

-	**Maintained by**:  
	[the Docker Community](https://github.com/Quantisan/docker-clojure)

-	**Supported architectures**: ([more info](https://github.com/docker-library/official-images#architectures-other-than-amd64))  
	[`amd64`](https://hub.docker.com/r/amd64/clojure/), [`arm32v5`](https://hub.docker.com/r/arm32v5/clojure/), [`arm32v7`](https://hub.docker.com/r/arm32v7/clojure/), [`arm64v8`](https://hub.docker.com/r/arm64v8/clojure/), [`i386`](https://hub.docker.com/r/i386/clojure/), [`ppc64le`](https://hub.docker.com/r/ppc64le/clojure/), [`s390x`](https://hub.docker.com/r/s390x/clojure/)

-	**Published image artifact details**:  
	[repo-info repo's `repos/clojure/` directory](https://github.com/docker-library/repo-info/blob/master/repos/clojure) ([history](https://github.com/docker-library/repo-info/commits/master/repos/clojure))  
	(image metadata, transfer size, etc)

-	**Image updates**:  
	[official-images PRs with label `library/clojure`](https://github.com/docker-library/official-images/pulls?q=label%3Alibrary%2Fclojure)  
	[official-images repo's `library/clojure` file](https://github.com/docker-library/official-images/blob/master/library/clojure) ([history](https://github.com/docker-library/official-images/commits/master/library/clojure))

-	**Source of this description**:  
	[docs repo's `clojure/` directory](https://github.com/docker-library/docs/tree/master/clojure) ([history](https://github.com/docker-library/docs/commits/master/clojure))

# What is Clojure?

Clojure is a dialect of the Lisp programming language. It is a general-purpose programming language with an emphasis on functional programming. It runs on the Java Virtual Machine, Common Language Runtime, and JavaScript engines. Like other Lisps, Clojure treats code as data and has a macro system.

> [wikipedia.org/wiki/Clojure](http://en.wikipedia.org/wiki/Clojure)

![logo](https://raw.githubusercontent.com/docker-library/docs/665526c3b12cedfd721234cedb61e8433f73b75a/clojure/logo.png)

# How to use this image

## Build tools

Clojure has three major approaches to building and running projects:

1.	[leiningen](https://leiningen.org)
	1.	The oldest and probably most common tool
2.	[boot](http://boot-clj.com)
	1.	An alternative approach that solves similar problems as leiningen
3.	[tools-deps](https://clojure.org/guides/deps_and_cli)
	1.	A more recent official tool for some of the lein/boot use cases

There are variants of this image for all three of these tools and their respective releases. The most basic form of these tags is:

1.	`clojure:lein`
2.	`clojure:boot`
3.	`clojure:tools-deps`

But you can also append a hyphen and the version of that tool you'd like to use. For example, for lein 2.8.1 you can use this image: `clojure:lein-2.8.1`.

## Run your app with leiningen

Add a `Dockerfile` to an existing Leiningen/Clojure project with the following contents:

```dockerfile
FROM arm64v8/clojure
COPY . /usr/src/app
WORKDIR /usr/src/app
CMD ["lein", "run"]
```

Then, run these commands to build and run the image:

```console
$ docker build -t my-clojure-app .
$ docker run -it --rm --name my-running-app my-clojure-app
```

While the above is the most straightforward example of a `Dockerfile`, it does have some drawbacks. The `lein run` command will download your dependencies, compile the project, and then run it. That's a lot of work, all of which you may not want done every time you run the image. To get around this, you can download the dependencies and compile the project ahead of time. This will significantly reduce startup time when you run your image.

```dockerfile
FROM arm64v8/clojure
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
COPY project.clj /usr/src/app/
RUN lein deps
COPY . /usr/src/app
RUN mv "$(lein uberjar | sed -n 's/^Created \(.*standalone\.jar\)/\1/p')" app-standalone.jar
CMD ["java", "-jar", "app-standalone.jar"]
```

Writing the `Dockerfile` this way will download the dependencies (and cache them, so they are only re-downloaded when the dependencies change) and then compile them into a standalone jar ahead of time rather than each time the image is run.

You can then build and run the image as above.

## Compile your Lein/Clojure project into a jar from within the container

If you have an existing Lein/Clojure project, it's fairly straightforward to compile your project into a jar from a container:

```console
$ docker run -it --rm -v "$PWD":/usr/src/app -w /usr/src/app arm64v8/clojure lein uberjar
```

This will build your project into a jar file located in your project's `target/uberjar` directory.

## More details

See [the official image README](https://github.com/Quantisan/docker-clojure/blob/master/README.md) for more details about using this image with boot and tools-deps.

# License

View [license information](http://clojure.org/license) for the software contained in this image.

As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).

Some additional license information which was able to be auto-detected might be found in [the `repo-info` repository's `clojure/` directory](https://github.com/docker-library/repo-info/tree/master/repos/clojure).

As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.
