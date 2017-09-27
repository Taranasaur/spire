[![Build Status](https://travis-ci.com/spiffe/spire.svg?token=pXzs6KRAUrxbEXnwHsPs&branch=master)](https://travis-ci.com/spiffe/spire)
[![Coverage Status](https://coveralls.io/repos/github/spiffe/spire/badge.svg?branch=master&t=GWBRCP)](https://coveralls.io/github/spiffe/spire?branch=master)

![SPIRE Logo](/doc/spire_logo.png)

SPIRE (the SPIFFE Runtime Environment) provides a toolchain that defines a central registry of
SPIFFE IDs (the Server), and a Node Agent that can be run adjacent to a workload and
exposes a local Workload API.


# Installing SPIRE

There are several ways to install the SPIRE binaries:

* Binary releases can be found at https://github.com/spiffe/spire/releases
* `go get github.com/spiffe/spire/...` will fetch and build all of SPIRE and its
  dependencies and install them in $GOPATH/bin
* [Building from source](/CONTRIBUTING.md)

# Configuring SPIRE

## SPIRE Agent  

SPIRE Agent runs on every node and is responsible for requesting certificates from the spire server,
attesting the validity of local workloads, and providing them SVIDs.

### SPIRE Agent configuration

The following details the configurations for the spire agent. The configurations can be set through
.conf file or passed as command line args, the command line configurations takes precedence.

 |Configuration          | Description                                                          |
 |-----------------------|----------------------------------------------------------------------|
 |BindAddress            |  The GRPC Address where the WORKLOAD API Service is set to listen    |
 |BindPort               |  The GRPC port where the WORKLOAD API Service is set to listen       |
 |DataDir                |  Directory where the runtime data will be stored                     |
 |LogFile                |  Sets the path to log file                                           |
 |LogLevel               |  Sets the logging level DEBUG|INFO|WARN|ERROR>                       |
 |PluginDir              |  Directory where the plugin configuration are stored                 |
 |ServerAddress          |  The GRPC Address where the SPIRE Server is running                  |
 |ServerPort             |  The GRPC port of the SPIRE Service                                  |
 |SocketPath             |  Sets the path where the socketfile will be generated                |
 |TrustBundlePath        |  Path to trusted CA Cert bundle                                      |
 |TrustDomain            |  SPIFFE trustDomain of the SPIRE Agent                               |


[default configuration file](/conf/agent/default_agent_config.conf)

```
BindAddress = "127.0.0.1"
BindPort = "8088"
DataDir = "."
LogLevel = "INFO"
PluginDir = "conf/plugin/agent"
ServerAddress = "127.0.0.1"
ServerPort = "8081"
SocketPath ="/tmp/agent.sock"
TrustBundlePath = "conf/agent/carootcert.pem"
TrustDomain = "example.org"
```


### SPIRE Agent commands

 |Command                   | Action                                                           |
 |--------------------------|------------------------------------------------------------------|
 |`spire-agent run`         |  Starts the SPIRE Agent                                          |

## SPIRE Server  

SPIRE Server is responsible for validating and signing all CSRs in the SPIFFE trust domain.
Validation is performed through platform-specific Attestation plugins, as well as policy enforcement
backed by the SPIRE Server datastore.

### SPIRE Server configuration

The following details the configurations for the spire server. The configurations can be set through
a .conf file or passed as command line args, the command line configurations takes precedence.

 |Configuration          | Description                                                          |
 |-----------------------|----------------------------------------------------------------------|
 |BaseSpiffeIDTTL        |  TTL that defines how long the generated Base SVID is valid          |
 |BindAddress            |  The GRPC Address where the SPIRE Service is set to listen           |
 |BindPort               |  The GRPC port where the SPIRE Service is set to listen              |
 |BindHTTPPort           |  The HTTP port where the SPIRE Service is set to listen              |
 |LogFile                |  Sets the path to log file                                           |
 |LogLevel               |  Sets the logging level DEBUG|INFO|WARN|ERROR>                       |
 |PluginDir              |  Directory where the plugin configuration are stored                 |
 |TrustDomain            |  SPIFFE trustDomain of the SPIRE Agent                               |

[default configuration file](/conf/server/default_server_config.conf)

```
BaseSpiffeIDTTL = 999999
BindAddress = "127.0.0.1"
BindPort = "8081"
BindHTTPPort = "8080"
LogLevel = "INFO"
PluginDir = "conf/plugin/server/"
TrustDomain = "example.org"
```

### SPIRE Server commands

 |Command                   | Action                                                           |
 |--------------------------|------------------------------------------------------------------|
 |`spire-server run`        |  Starts the SPIRE Server                                         |

# Community

The SPIFFE community, and [Scytale](https://scytale.io) in particular, maintain the SPIRE project.
Information on the various SIGs and relevant standards can be found in
https://github.com/spiffe/spiffe.

The SPIFFE and SPIRE governance policies are detailed in [GOVERNANCE](https://github.com/spiffe/spiffe/blob/master/GOVERNANCE.md)
