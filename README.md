CoreGI
=========

![DockerHub Stats](http://dockeri.co/image/yodlr/coregi)

WebUI for monitoring CoreOS clusters including fleet and etcd

![CoreGI](https://raw.githubusercontent.com/yodlr/CoreGI/master/site/img/coregi_logo.png)

Built with love by the [Yodlr](https://getyodlr.com) team

### What is CoreGI

CoreGI came out of our need for a one-stop dashboard for viewing the status of the applications running in our CoreOS clusters, monitoring etcd keys, and managing rolling software updates. We're pro cli-tools, but have found that simple web-apps provide improved visibility into complex systems.

![CoreGI Dashboard](https://raw.githubusercontent.com/yodlr/CoreGI/master/docs/images/coregi-units.png)

### CoreGI runs in CoreOS

CoreGI was created to be as simple as possible and deploying CoreGI is as easy as running a docker container. CoreGI can also be installed into a __CoreOS cluster__ using a CoreOS service file. Take a look at our CoreOS [service file][coregi_service] for an example. CoreGI can also be ran as an application using Node.js by using environment variables to change the default options, see [Getting Started](#getting-started).

We have setup automated Docker Hub builds for CoreGI [here](https://registry.hub.docker.com/u/yodlr/coregi/)


### Getting Started

##### CoreOS

```
git clone https://github.com/yodlr/CoreGI.git
cd CoreGI
fleetctl start services/coregi.service
```

Our example service file is setup to be a Global service listening on port 3000.  This can be modified in the CoreOS service file which can be found [here][coregi_service].

##### Docker

```
$ docker run --name coregi -p 3000:3000 yodlr/coregi:latest
```

##### Node.js

To change default options, see [options](#coregi-options).
Example with custom option:

```
$ FLEET_BINARY=/usr/local/bin/fleetctl npm start
```

### CoreGI Options

CoreGI default options. To change the default options, simply set the value of any of the following environment variables.

```
PORT = 3000
FLEET_BINARY = '/usr/bin/fleetctl'
FLEET_TUNNEL = '172.17.42.1'  //If set, will remove FLEET_ENDPOINT option.
FLEET_ENDPOINT = 'http://172.17.42.1:4001'
ETCD_HOST = '172.17.42.1'
ETCD_PORT = 4001
LOG_LEVEL = 'info'
```

### CoreGI Features

CoreGI currently supports querying Fleet for listing of __machines__, __units__, __unit-files__ and Etcd for listing of __keys__.
CoreGI also exposes a __REST API__ with the following endpoints:

* GET /api/machines
* GET /api/units
* GET /api/unitFiles
* GET /api/keys

#### Future Features

Some of the features we're thinking/planning on implementing include:

* Unit logs
* Unit status
* Start/stop/load/unload units
* Monitoring and editing etcd keys
* Rolling deployment of units


#### CoreGI is built with:

* [Node.js](http://nodejs.org/)
* [AngularJS](https://angularjs.org/)
* [Bootstrap](http://getbootstrap.com/)
* [Docker](https://www.docker.com/)



[coregi_service]: https://github.com/yodlr/CoreGI/blob/master/services/coregi.service
