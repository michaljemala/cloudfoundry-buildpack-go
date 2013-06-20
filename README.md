# Cloudfoundry Buildpack: Go

This is an experimental [Cloudfoundry buildpack][cloudfoundry-buildpack] for [Go][go].

It is heavily based on existing [Heroku Buildpack][heroku-buildpack] created by Keith Rarick. However it has to be modified to accomodate to the fact that the current CF v2 stack does not come with installed Python headers. Therefore Mercurial as well as Bazaar needs to be installed as a pure Python libs, i.e. without native C bindings.

In order to speed things up a bit the [compile][compile] script caches Go binaries as well as the Mercurial and Bazaar sources.

Besides the actual source code, the following files must be present in the root folder of your application:
* .godir - contains the desired name of the final binary
* Procfile - specify the type of the application and the actual command executed when the instance is started

##Example
```
$ git clone https://github.com/michaljemala/hello-go.git
$ cd hello-go/
$  cf push --buildpack https://github.com/michaljemala/cloudfoundry-buildpack-go.git --name <APP_NAME> --instances 1 --memory 64M --domain cfapps.io --host <APP_NAME> --force
Creating <APP_NAME>... OK

Binding <SUBDOMAIN_NAME>.cfapps.io to <APP_NAME>... OK
Uploading <APP_NAME>... OK
Starting <APP_NAME>... OK
-----> Downloaded app package (4.0K)
Initialized empty Git repository in /tmp/buildpacks/cloudfoundry-buildpack-go.git/.git/
Installing cloudfoundry-buildpack-go.git.
-----> Installing Go 1.1.1... done in 47s
-----> Installing Virtualenv... done
-----> Downloading Mercurial sources... done in 19s
-----> Installing Mercurial... done
-----> Downloading Bazaar sources... done in 12s
-----> Installing Bazaar... done
-----> Running 'go get -tags cf ./...'... done in 31s
-----> Uploading staged droplet (1.4M)
-----> Uploaded droplet
Checking <APP_NAME>...
Staging in progress...
Staging in progress...
Staging in progress...
  0/1 instances: 1 starting
  1/1 instances: 1 running
OK
$ curl -I http://<SUBDOMAIN_NAME>.cfapps.io/
HTTP/1.1 200 OK
Transfer-Encoding: chunked
Connection: keep-alive
Date: Wed, 19 Jun 2013 17:36:42 GMT
Server: XMS (724Solutions HTA XMP_40_M2_B083 20091027.165340)
```

[go]: http://golang.org/
[cloudfoundry-buildpack]: http://docs.cloudfoundry.com/docs/using/deploying-apps/buildpacks.html
[heroku-buildpack]: https://github.com/kr/heroku-buildpack-go.git
[compile] [https://github.com/michaljemala/cloudfoundry-buildpack-go/blob/master/bin/compile]
