# Cloudfoundry Buildpack: Go

This is an experimental [Cloudfoundry buildpack][cloudfoundry-buildpack] for [Go][go].

It is heavily based on existing [Heroku Buildpack][heroku-buildpack] created by Keith Rarick. However it had to be modified to accomodate to the fact that the current CF v2 stack does not come with installed Python header files. Therefore Mercurial, as well as Bazaar, needs to be installed as a pure Python libs, i.e. without native C bindings.

In order to speed things up a bit the [compile][compile] script caches Go binaries as well as the Mercurial and Bazaar sources.

Besides the actual source code, the following files must be present in the root folder of your application:
* .godir - contains the desired name of the final binary
* Procfile - specifies the type of the application and the actual command executed when the instance is started

##godep support

This buildpack includes support for optionally using [godep][godep]. If your repository includes a `Godeps` file created via:

```
$ godep save -copy=false
```

..then the buildpack will `go get` the godep tool, run `godep restore`, and `go install` on your app before finalizing the droplet.

##Example
```
$ git clone https://github.com/michaljemala/hello-go.git
$ cd hello-go/
$ cf push
Using manifest file /Users/misiak/Work/Projects/Go/src/github.com/michaljemala/hello-go/manifest.yml

Creating app hello-go in org mjemala-org / space development as mjemala@gopivotal.com...
OK

Creating route hello-go-trigonal-hauerite.cfapps.io...
OK

Binding hello-go-trigonal-hauerite.cfapps.io to hello-go...
OK

Uploading hello-go...
Uploading app files from: /Users/misiak/Work/Projects/Go/src/github.com/michaljemala/hello-go
Uploading 1.6K, 4 files
OK

Starting app hello-go in org mjemala-org / space development as mjemala@gopivotal.com...
OK
-----> Downloaded app package (4.0K)
Cloning into '/tmp/buildpacks/cloudfoundry-buildpack-go'...
 Installing Go 1.2.1...  done in 5s
 Installing Virtualenv...  done
 Downloading Mercurial sources...  done in 1s
 Installing Mercurial...  done
 Downloading Bazaar sources...  done in 14s
 Installing Bazaar...  done
 Running 'go get -tags cf ./...'...  done in 33s
-----> Uploading droplet (2.0M)

0 of 1 instances running, 1 down
0 of 1 instances running, 1 down
1 of 1 instances running

App started

Showing health and status for app hello-go in org mjemala-org / space development as mjemala@gopivotal.com...
OK

requested state: started
instances: 1/1
usage: 8M x 1 instances
urls: hello-go-trigonal-hauerite.cfapps.io

     state     since                    cpu    memory       disk
#0   running   2014-04-26 11:10:07 AM   0.0%   7.9M of 8M   7.9M of 1G
$ curl -I http://hello-go-trigonal-hauerite.cfapps.io/
HTTP/1.1 200 OK
Content-length: 955
Content-Type: text/plain; charset=utf-8
Date: Sat, 26 Apr 2014 17:13:16 GMT
Connection: keep-alive
```

[go]: http://golang.org/
[cloudfoundry-buildpack]: http://docs.cloudfoundry.com/docs/using/deploying-apps/buildpacks.html
[heroku-buildpack]: https://github.com/kr/heroku-buildpack-go.git
[compile]: https://github.com/michaljemala/cloudfoundry-buildpack-go/blob/master/bin/compile
[godep]: https://github.com/tools/godep
