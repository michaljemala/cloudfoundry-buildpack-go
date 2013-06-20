# Cloudfoundry Buildpack: Go

This is an experimental [Cloudfoundry buildpack][cloudfoundry-buildpack] for [Go][go].

It is based on existing [Heroku Buildpack][heroku-buildpack] created by Keith Rarick.

##Example
```
$ git clone https://github.com/michaljemala/hello-go.git
$ cd hello-go/
$ cf push --buildpack https://github.com/michaljemala/cloudfoundry-buildpack-go.git --name <APP_NAME> --instances 1 --memory 64M --domain cfapps.io --host <SUBDOMAIN_NAME> --force
Creating hello-go... OK

Binding hello-go.cfapps.io to hello-go... OK
Uploading hello-go... OK
Starting hello-go... OK
-----> Downloaded app package (4.0K)
Initialized empty Git repository in /tmp/buildpacks/cloudfoundry-buildpack-go.git/.git/
Installing cloudfoundry-buildpack-go.git.
-----> Installing Go 1.1.1... done
Python 2.6.5
-----> Running: go get -tags heroku ./...
-----> Uploading staged droplet (1.3M)
-----> Uploaded droplet
Checking hello-go...
Staging in progress...
Staging in progress...
Staging in progress...
Staging in progress...
Staging in progress...
  0/1 instances: 1 down
  0/1 instances: 1 starting
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
