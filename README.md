# Cloudfoundry Buildpack: Go

This is an experimental [Cloudfoundry buildpack][cloudfoundry-buildpack] for [Go][go].

It is based on existing [Heroku Buildpack][heroku-buildpack] created by Keith Rarick.

NOTE: The Mercurial and Bazaar support is not available at the moment because of issues with current CFv2 instance which is missing python-dev package and therefore the native bindings of both version control systems cannot be built.

[go]: http://golang.org/
[cloudfoundry-buildpack]: http://docs.cloudfoundry.com/docs/using/deploying-apps/buildpacks.html
[heroku-buildpack]: https://github.com/kr/heroku-buildpack-go.git
