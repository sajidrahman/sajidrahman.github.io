---
title: Deploying in Apache Tomcat via Maven-Tomcat plugin

# Summary for listings and search engines
summary: In this post we will present some useful Latex hacks that come handy in academic writing.

# Link this post with a project
projects: []

# Date published
date: "2020-12-13T00:00:00Z"

# Date updated
lastmod: "2020-08-13T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- admin

tags: [java, maven, tomcat, maven-tomcat-plugin, deployment]


categories:
- How-to
---

1. Add the following user-roles and user (specially a user with roles of ```manager-jmx,manager-script```, see 'maven' user, for example) in tomcat-users.xml file. (Sidenote: you can create a user with ```manager-gui``` role to access Tomcat manager interface from your browser, that's pretty cool and handy!!)

```xml
<!--This file is located in %TOMCAT_HOME%/conf/tomcat-users.xml -->
<?xml version='1.0' encoding='utf-8'?>
<tomcat-users>

  <role rolename="manager-gui"/>
  <role rolename="manager-script"/>
  <role rolename="manager-jmx"/>
  <user username="admin" password="tomcat" roles="manager-gui"/>
  <user username="maven" password="tomcat" roles="manager-jmx,manager-script"/>

</tomcat-users>
```

2. Add above Tomcat’s user ('maven' user in this case) in the Maven setting file, later Maven will use this user to login Tomcat server.( N.B. In case of a project running in IntelliJ, view/create maven settings.xml file from POM --> MAVEN --> Open Settings.xml (Or Create Settings.xml, if settings.xml is not present).)


```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
    <servers>

        <server>
            <id>TomcatServer</id>
            <username>root</username>
            <password>tomcat</password>
        </server>

    </servers>
</settings>
```

3. Declare a maven-tomcat plugin in pom.xml.

```xml
	<plugin>
		<groupId>org.apache.tomcat.maven</groupId>
		<artifactId>tomcat7-maven-plugin</artifactId>
		<version>2.2</version>
		<configuration>
			<url>http://localhost:8080/manager/text</url>
			<server>TomcatServer</server>
			<path>/mycoolapp</path>
		</configuration>
	</plugin>
```

Here, we are configuring maven-tomcat plugin to access TomcatServer with credentials defined in maven's settings.xml file and deploy our app in this context path **/mycoolapp**.

4. Run Tomcat Server (from command line `%TOMCAT_HOME%/bin/startup.sh`).

5. Now execute this command in terminal after going to your project directory: ```maven tomcat7:deploy``` to deploy your war file in Tomcat. You should get a **BUILD SUCCESS** message if everything goes well.
