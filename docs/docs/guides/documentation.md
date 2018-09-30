# Documentation System

This guide details how this documentation system is setup and hosted

I've been looking for an easy to use way to store notes, so that they can be viewed online and edited from anywhere.
I'm not sure this is the best solution to this problem, however it's better than what I had before (nothing)

## Source

The source of this documentation is hosted on github at <https://github.com/AaronFoley/docs>

Hosting the source in git allows me to access it from anywhere on the internet and easily update it.
As this uses simple markdown files, it is really easy to edit as well

## Hosting

This web interface is hosted within my Lab Openshift cluster, passing through the external nginx proxy.

The docker image is built using [Openshifts Source 2 Image](https://docs.okd.io/3.10/dev_guide/builds/index.html) builds system.
It uses the provided openshift/python:3.6 builder image to install mkdocs and other requirements such as the theme.

Using the `APP_SCRIPT` environment variable, the containers command is set to run mkdocs server listening on port 8080.
A route is then exposed from the Openshift router allowing me to access documents over HTTPS

Openshift supports buidling and deploying automatically via webhook. Once I've pushed my changes to my github repository a
new image is built containing the source code and automatically deployed.
