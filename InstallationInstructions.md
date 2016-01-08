

# Requirements #

For running the Signavio Core Components, you need the following software components:

  * Java 5 JDK or higher
  * Apache Tomcat 6 or higher OR JBoss application aerver
  * An environment for running Apache Ant build scripts (we recommend using the IDE Eclipse for Java EE)

Furthermore, you have to [checkout the Signavio Core Components](http://code.google.com/p/signavio-core-components/source/checkout) source code.

# UTF-8 Encoding Configuration #

A lot of users face issues regarding an invalid encoding that may result in corrupted model files. That is why it is very important that you ensure the usage of UTF-8 encoding in the whole application stack.

## Eclipse Configuration ##

If you use Eclipse for building the source code, make sure that your workspace is configured to use UTF-8 as well as Windows file delimiter. You find these settings in the "Workspace" panel in the Eclipse preferences.

## Apache Tomcat Configuration ##

First, you have to ensure that URL are interpreted in UTF-8 encoding. Open the file `conf/server.xml` and add the attribute `URIEncoding="UTF-8"` to the HTTP connector. Example:
```
<Connector URIEncoding="UTF-8" connectionTimeout="20000" port="8080" protocol="HTTP/1.1" redirectPort="8443"/>
```

Second, you have to ensure that all files are read and written in UTF-8 encoding. To apply this, you have to set the JVM parameter `-Dfile.encoding=UTF-8`. You can set this parameter by editing the variable `JAVA_OPTS` in the file `bin/catalina.bat` (on Windows) or `bin/catalina.sh` (on Linux).

# Configuration #

If you meet all requirements, the only file you have to edit is `build.properties` in the project's root directory. The file contains comments for all configuration properties. The following properties can be edited:

  * **dir-tomcat-webapps**
    * The path to your Apache Tomcat webapps folder. Only required, if you want to deploy to an Apache Tomcat web server.
  * **dir-jboss-webapps**
    * The path to your jBoss deployment folder. Only required, if you want to deploy to a JBoss application server.
  * **target**
    * The folder the war file(s) is/are stored. You usually don't have to change this.
  * **version**
    * The version of the application. If you want to integrate the Signavio Core Components into your own software product, you can align the version number. The version number is used in the loading splash screens of the client components.
  * **war**
    * The name of the war file, if you use the all-in-one-war build target (explained in the next section).
  * **configuration**
    * The configuration you want to use. This is the name of the folder in the _configuration_ project that contains the configuration and skin files. The following configurations are available: default, Activiti, jBPM. You can also add your own configuration in the _configuration_ project.
  * **host**
    * The URL of your server. Format: `http(s)://<domain>(:<port>)`
    * Do not add a trailing slash!
    * Example: `http://localhost:8080`
  * **fileSystemRootDirectory**
    * The path on your system the directories and diagram files are stored.
    * Do not use \ ! Always use / !
    * Do not add a trailing slash!
    * Example: `C:/repository`

# Build and deploy #

For building and deploying the Signavio Core Components you only have to execute a target in the `build.xml` Ant build script in the project's root directory. There are two different build types available: the all-in-one-war build and the separate-war-files build. The all-in-one-war build can be deployed to Tomcat and JBoss, the separate-war-files can currently only be deployted to Tomcat.

## Build and deploy the all-in-one-war ##

For building the all-in-one-war and deploying to Tomcat, use the following Ant target:
```
ant build-and-deploy-all-in-one-war-to-tomcat
```

For building the all-in-one-war and deploying to JBoss, use the following Ant target:
```
ant build-and-deploy-all-in-one-war-to-jboss
```

The war file's name is the name specified in the configuration file.

## Build and deploy separate-war-files ##

For building the separate-war-files and deploying to Tomcat, use the following Ant target:
```
ant build-and-deploy-all-war-files-to-tomcat
```

Note that you cannot change the war files' names. The following war files will be deployed:
  * `ROOT.war`
  * `editor.war`
  * `explorer.war`
  * `libs.war`

# Run the Signavio Core Components #

To access the Signavio Core Components, open the following URL in your browser:

`http://<yourserver>(:<port>)(/<all-in-one-war-file-name>)/p/explorer`

If you use the all-in-one-war build, the name of the war file is the prefix of the URL's path. The default URL is http://localhost:8080/signaviocore/p/explorer . If you deploy the components in separate war files, the file-based backend is deployed as the ROOT project so that its URL has not path prefix (Example: http://localhost:8080/p/explorer ).