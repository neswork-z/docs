<!--

********************************************************************************

WARNING:

    DO NOT EDIT "traefik/README.md"

    IT IS AUTO-GENERATED

    (from the other files in "traefik/" combined with a set of templates)

********************************************************************************

-->

# Supported tags and respective `Dockerfile` links

-	[`v2.0.0-rc2`, `2.0.0-rc2`, `v2.0`, `2.0`, `montdor`](https://github.com/containous/traefik-library-image/blob/5de2ba0bde779c08d99a87f70cf46fd24c185f68/scratch/Dockerfile)
-	[`v2.0.0-rc2-alpine`, `2.0.0-rc2-alpine`, `v2.0-alpine`, `2.0-alpine`, `montdor-alpine`](https://github.com/containous/traefik-library-image/blob/5de2ba0bde779c08d99a87f70cf46fd24c185f68/alpine/Dockerfile)
-	[`v1.7.14`, `1.7.14`, `v1.7`, `1.7`, `maroilles`, `latest`](https://github.com/containous/traefik-library-image/blob/1220871969fc11f5e619bba4de3355e695fe3061/scratch/arm64/Dockerfile)
-	[`v1.7.14-alpine`, `1.7.14-alpine`, `v1.7-alpine`, `1.7-alpine`, `maroilles-alpine`, `alpine`](https://github.com/containous/traefik-library-image/blob/1220871969fc11f5e619bba4de3355e695fe3061/alpine/Dockerfile)

[![arm64v8/traefik build status badge](https://img.shields.io/jenkins/s/https/doi-janky.infosiftr.net/job/multiarch/job/arm64v8/job/traefik.svg?label=arm64v8/traefik%20%20build%20job)](https://doi-janky.infosiftr.net/job/multiarch/job/arm64v8/job/traefik/)

# Quick reference

-	**Where to get help**:  
	[the Docker Community Forums](https://forums.docker.com/), [the Docker Community Slack](https://blog.docker.com/2016/11/introducing-docker-community-directory-docker-community-slack/), or [Stack Overflow](https://stackoverflow.com/search?tab=newest&q=docker)

-	**Where to file issues**:  
	[https://github.com/containous/traefik-library-image/issues](https://github.com/containous/traefik-library-image/issues)

-	**Maintained by**:  
	[the Traefik Project](https://github.com/containous/traefik-library-image)

-	**Supported architectures**: ([more info](https://github.com/docker-library/official-images#architectures-other-than-amd64))  
	[`amd64`](https://hub.docker.com/r/amd64/traefik/), [`arm32v6`](https://hub.docker.com/r/arm32v6/traefik/), [`arm64v8`](https://hub.docker.com/r/arm64v8/traefik/), [`windows-amd64`](https://hub.docker.com/r/winamd64/traefik/)

-	**Published image artifact details**:  
	[repo-info repo's `repos/traefik/` directory](https://github.com/docker-library/repo-info/blob/master/repos/traefik) ([history](https://github.com/docker-library/repo-info/commits/master/repos/traefik))  
	(image metadata, transfer size, etc)

-	**Image updates**:  
	[official-images PRs with label `library/traefik`](https://github.com/docker-library/official-images/pulls?q=label%3Alibrary%2Ftraefik)  
	[official-images repo's `library/traefik` file](https://github.com/docker-library/official-images/blob/master/library/traefik) ([history](https://github.com/docker-library/official-images/commits/master/library/traefik))

-	**Source of this description**:  
	[docs repo's `traefik/` directory](https://github.com/docker-library/docs/tree/master/traefik) ([history](https://github.com/docker-library/docs/commits/master/traefik))

![logo](https://raw.githubusercontent.com/docker-library/docs/a6cc2c5f4bc6658168f2a0abbb0307acaefff80e/traefik/logo.png)

[Traefik](https://github.com/containous/traefik) is a modern HTTP reverse proxy and load balancer that makes deploying microservices easy.

Traefik integrates with your existing infrastructure components ([Docker](https://www.docker.com/), [Swarm mode](https://docs.docker.com/engine/swarm/), [Kubernetes](https://kubernetes.io), [Marathon](https://mesosphere.github.io/marathon/), [Consul](https://www.consul.io/), [Etcd](https://coreos.com/etcd/), [Rancher](https://rancher.com), [Amazon ECS](https://aws.amazon.com/ecs), ...) and configures itself automatically and dynamically.

Telling Traefik where your orchestrator is could be the *only* configuration step you need to do.

# Example usage

Grab a [sample configuration file](https://raw.githubusercontent.com/containous/traefik/master/traefik.sample.toml) and rename it to `traefik.toml`. Enable `docker` provider and web UI:

```toml
################################################################
# API and dashboard configuration
################################################################
[api]
################################################################
# Docker configuration backend
################################################################
[docker]
domain = "docker.local"
watch = true
```

Start Traefik:

```bash
docker run -d -p 8080:8080 -p 80:80 \
-v $PWD/traefik.toml:/etc/traefik/traefik.toml \
-v /var/run/docker.sock:/var/run/docker.sock \
traefik
```

Start a backend server, named `test`:

```bash
docker run -d --name test emilevauge/whoami
```

And finally, you can access to your `whoami` server throught Traefik, on the domain name `{containerName}.{configuredDomain}`:

```bash
curl --header 'Host: test.docker.local' 'http://localhost:80/'
Hostname: 117c5530934d
IP: 127.0.0.1
IP: ::1
IP: 172.17.0.3
IP: fe80::42:acff:fe11:3
GET / HTTP/1.1
Host: 172.17.0.3:80
User-Agent: curl/7.35.0
Accept: */*
Accept-Encoding: gzip
X-Forwarded-For: 172.17.0.1
X-Forwarded-Host: 172.17.0.3:80
X-Forwarded-Proto: http
X-Forwarded-Server: f2e05c433120

```

The web UI [http://localhost:8080](http://localhost:8080) will give you an overview of the frontends/backends and also a health dashboard.

![Web UI Providers](https://raw.githubusercontent.com/containous/traefik/master/docs/img/web.frontend.png)

# Documentation

You can find the complete documentation at [https://docs.traefik.io](https://docs.traefik.io).

A collection of contributions around Traefik can be found at [https://awesome.traefik.io](https://awesome.traefik.io).

# License

View [license information](https://github.com/containous/traefik/blob/master/LICENSE.md) for the software contained in this image.

As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).

Some additional license information which was able to be auto-detected might be found in [the `repo-info` repository's `traefik/` directory](https://github.com/docker-library/repo-info/tree/master/repos/traefik).

As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.
