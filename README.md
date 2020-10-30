# Imply Maven Repository

Update your projects to use Imply netty artifact stored in Imply Artifactory.

### ~/.m2/settings.xml

```
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
    ...
    <servers>
        <server>
            <username>eng</username>
            <password>AP8cigvgtfjXGXLig7xcFUCWqJG</password>
            <id>repo.qa.imply.io</id>
        </server>
    </servers>
    ...
</settings>
```

### pom.xml (in implydata/druid project, for example)

```
...

    <dependencies>
    ...
        <dependency>
            <groupId>io.netty</groupId>
            <artifactId>netty</artifactId>
            <version>3.10.6.Final-iap3</version>
        </dependency>
    </dependencies>

    <repositories>
        <repository>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
            <id>repo.qa.imply.io</id>
            <name>libs-release</name>
            <url>https://repo.qa.imply.io:443/artifactory/libs-release</url>
        </repository>
    </repositories>
</project>
```



# Imply Releases

To create a new build to be used in Imply releases, checkout the release branch (eg: 3.10.6.Final-iap), then run

```
mvn -DreleaseVersion=<RELEASE_VERSION> -DdevelopmentVersion=<DEV_VERSION>-SNAPSHOT -DpushChanges=false -Dgpg.skip -Darguments="-Dgpg.skip" clean release:clean release:prepare
git push imply netty-<RELEASE_VERSION>
git push imply <RELEASE_BRANCH>
```

This will run all tests, and takes about 3.5 minutes to run.

The tag can now be used in the distribution repo when creating an Imply release.

# Netty Project

Netty is an asynchronous event-driven network application framework for rapid development of maintainable high performance protocol servers & clients.

## Links

* [Web Site](http://netty.io/)
* [Downloads](http://netty.io/downloads.html)
* [Documentation](http://netty.io/wiki/)
* [@netty_project](https://twitter.com/netty_project)

## How to build

For the detailed information about building and developing Netty, please visit [the developer guide](http://netty.io/wiki/developer-guide.html).  This page only gives very basic information.

You require the following to build Netty:

* Latest stable [Oracle JDK 7](http://www.oracle.com/technetwork/java/)
* Latest stable [Apache Maven](http://maven.apache.org/)

Note that this is build-time requirement.  JDK 5 (for 3.x) or 6 (for 4.0+) is enough to run your Netty-based application.

## Branches to look

[The 'master' branch](https://github.com/netty/netty/tree/master) is where the development of the latest major version lives on.  The development of all other versions takes place in each branch whose name is identical to `<majorVersion>.<minorVersion>`.  For example, the development of 3.9 and 4.0 resides in [the branch '3.9'](https://github.com/netty/netty/tree/3.9) and [the branch '4.0'](https://github.com/netty/netty/tree/4.0) respectively.
