#Heroku

One of the most popular PaaS (Platform as a Service) vendor. It was founded in the year 2007 and started by offer a PaaS for the Ruby languages. Since them they have wide support of different languages for example Java, NodeJs, Python, PHP and
many more. They offer also the possibility to extends the supported languages by writing your own Buildpacks. A Buildpack is a collection of files that use Heroku to compile and deploy an application. 

What Heroku make it so special is that it compiles and build the application from the source code and deploy the binary atrifacts after this build phase. This is different from other approaches where you deploy the binary artifacts after you build it on a build machine or something else.

##Buildpack

A Buildpack contains three files that are reasponsable for compile and start an application.

* bin/detect
* bin/compile
* bin/release 

Heroku has following default buildpacks that support these languages.

* Ruby		https://github.com/heroku/heroku-buildpack-ruby
* Node.js	https://github.com/heroku/heroku-buildpack-nodejs
* Clojure	https://github.com/heroku/heroku-buildpack-clojure
* Python	https://github.com/heroku/heroku-buildpack-python
* Java		https://github.com/heroku/heroku-buildpack-java
* Gradle	https://github.com/heroku/heroku-buildpack-gradle
* Grails	https://github.com/heroku/heroku-buildpack-grails
* Scala		https://github.com/heroku/heroku-buildpack-scala
* Play		https://github.com/heroku/heroku-buildpack-play
* PHP		https://github.com/heroku/heroku-buildpack-php


###Custom Buildpack

To write your own buildpack you have to create a Github project that contains three files.

* bin/detect	Determines whether to apply this buildpack to an app.
* bin/compile	Used to perform the transformation steps on the app.
* bin/release	Provides metadata back to the runtime.

An example for a custom buildpack to support applications written in the [D programming language](http://dlang.org/) can be found [here](https://github.com/pussinboots/heroku-buildpack-d). It could also be used as a starting point to write your own buildpack for your flavored language.

###Multiple Buildpacks 

With the concepts of buildpacks there it is also possible to deploy applications to heroku there use different languages and framworks. 

Imagine you have an web application that manage it frontend dependencies with the [bower](http://bower.io/) package manager and the backend is implemented with the play 2 framework and the scala language. That application need a nodejs and a sbt runtime. For a local development you can install this runtimes by your own. But Heroku need these runtimes also to build and deploy this application. 

In a normal scenario you could only specify one buildpack per application. Thanks to David Dollar he implements a build pack for heroku called [heroku buildpack multi](https://github.com/ddollar/heroku-buildpack-multi) that allows you to specify so many buildpacks you need. 

Step by step

first you configure the multi buildpack

```bash
heroku config:add BUILDPACK_URL=https://github.com/ddollar/heroku-buildpack-multi.git
```

Than add a file .buildpacks to the root of your github project. So to 

* [nodejs build pack](https://github.com/heroku/heroku-buildpack-nodejs.git)
* [scala (play 2) build pack](https://github.com/heroku/heroku-buildpack-scala.git)

```bash
heroku config:add BUILDPACK_URL=https://github.com/ddollar/heroku-buildpack-multi.git
```

The .buildpacks file
```bash
https://github.com/heroku/heroku-buildpack-nodejs.git
https://github.com/heroku/heroku-buildpack-scala.git
```

Done.
