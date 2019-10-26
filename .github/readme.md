Drone is a Continuous Delivery system built on container technology. Drone uses a simple YAML configuration file, a superset of docker-compose, to define and execute Pipelines inside Docker containers. 

<br/>

<img src="https://github.com/drone/brand/blob/master/screenshots/screenshot_build_success.png" style="max-width:100px;" />

Sample Pipeline Configuration:

```yaml
name: default

kind: pipeline
type: docker

steps:
- name: backend
  image: golang
  commands:
    - go get
    - go build
    - go test

- name: frontend
  image: node:6
  commands:
    - npm install
    - npm test

- name: publish
  image: plugins/docker
  settings:
    repo: octocat/hello-world
    tags: [ 1, 1.1, latest ]
    registry: index.docker.io

- name: notify
  image: plugins/slack
  settings:
    channel: developers
    username: drone
```

Documentation and Other Links:

* Setup Documentation [docs.drone.io/installation](http://docs.drone.io/installation/)
* Usage Documentation [docs.drone.io/getting-started](http://docs.drone.io/getting-started/)
* Plugin Index [plugins.drone.io](http://plugins.drone.io/)
* Getting Help [discourse.drone.io](https://discourse.drone.io)
* Build the Enterprise Edition [BUILDING](https://github.com/drone/drone/blob/master/BUILDING)
* Build the Community Edition [BUILDING_OSS](https://github.com/drone/drone/blob/master/BUILDING_OSS)

_Please note the official Docker images run the Drone Enterprise distribution. If you would like to run the Community Edition you can build from source by following the instructions in [BUILDING_OSS](https://github.com/drone/drone/blob/master/BUILDING_OSS)._


### IBM LSF Feature

1. Enable with Environment variable
```sh
export DRONE_LSF_ENABLED=true
export DRONE_LSF_HOME=/home/lsf
export DRONE_AGENTS_DISABLED=true
```

`DRONE_LSF_HOME` will be LSF's working directory

Example environment setup:

```sh
export DRONE_SERVER_HOST=127.0.0.1:8080
export DRONE_SERVER_PORT=:8080
export DRONE_GITEA_SERVER=http://127.0.0.1:3000/
export DRONE_GIT_ALWAYS_AUTH=false
export DRONE_GITEA_PRIVATE_MODE=false
export DRONE_GITEA_CLIENT_ID=cbc1c1aa-0bcf-4564-b332-bdc7c33c574a
export DRONE_GITEA_CLIENT_SECRET=14ul4UNSdmh-P8TQP6DLguRS0DZZZN7UbOoW1YU_4Nw=
export DRONE_RUNNER_CAPACITY=10
export DRONE_SERVER_PROTO=http
export DRONE_BASE=/
export DRONE_AGENTS_DISABLED=true
export DRONE_LSF_ENABLED=true
export DRONE_LSF_HOME=/home/lsf
```

> Notice that this feature only support single server mode.

2. PROXY (with base URL)

To enable proxy with base URL, set:

```
export DRONE_BASE=/drone
```

You have to rebuild drone-ui, please refer to [blueworrybear/drone-ui](https://github.com/blueworrybear/drone-ui)
