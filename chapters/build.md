#Build Management

##SBT Build

The [sbt](http://www.scala-sbt.org/) build tool is used to build the play backend part of this application. With a little trick we will integrate npm task execution into sbt build lifecycle management.

\begin{codelisting}
\codecaption{npm play un hook}
\label{code:npmplay}
```scala
object NPMPlayRunHook {
  import java.net.InetSocketAddress
  import play.PlayRunHook
  import sbt._
  import sbt.Keys._
 
  def apply(): PlayRunHook = {
    new PlayRunHook {
      override def beforeStarted(): Unit = {
        val cmdNpm = Seq("sh", "-c", "npm install")
        (cmdNpm  #||  "echo npm is missing and needed for local development to fetch the nodejs and bower dependencies. For install look here https://github.com/npm/npm. Perform npm task manual from your command line. Ignore it during herku deployment npm install will be performed fro the nodejs buildpack." !)
        /*val cmdCoffee = Seq("./node_modules/coffee-script/bin/coffee", "-c", "-o", "public/js/bankapp/coffee", "public/js/bankapp/coffee")
        (cmdCoffee  #||  "echo npm is missing and needed for local development to fetch the nodejs and bower dependencies. For install look here https://github.com/npm/npm. Perform npm task manual from your command line. Ignore it during herku deployment npm install will be performed fro the nodejs buildpack." !)*/
        println(s"++++ perform npm install when npm command can be found") 
      }
 
      override def afterStarted(address: InetSocketAddress): Unit = {
      }
 
      override def afterStopped(): Unit = {
      }
    }
  }
}
```
\end{codelisting}

With the code below you can register own [PlayRunHook](https://github.com/playframework/playframework/blob/master/framework/src/sbt-plugin/src/main/scala/play/PlayRunHooks.scala) implementations.
\begin{codelisting}
\codecaption{npm build.sbt}
\label{code:npmsbt}
```scala
playRunHooks <+= baseDirectory.map(base => NPMPlayRunHook())
```
\end{codelisting}

That setup perform npm install now every time when play is stated in run mode and code reloading is executed.
##NPM

The [npm](https://www.npmjs.org/) is the build tool for nodejs javascript projectsand very simple to configure and to use.  

##Travis CI

###Setup Build

###Multilanguage Build

###Integration

####Github

####Coveralls

####Unitcover ???

####Heroku
