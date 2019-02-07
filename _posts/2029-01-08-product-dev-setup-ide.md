---
layout: post
title: "Setup for tech11 Product Development"
date: 2019-01-09 10:12:44 +0100
tags: blog 
lang: en
author: houda
---
Setup Software Development Environment for tech11 Product Development
=====================================================================

## SOFTWARE

* JDK 1.8
* maven (latest)
* Docker (latest)

## IDEs

* eclipse (distribution Eclipse IDE for Enterprise Java Developers)
  https://www.eclipse.org/downloads/packages/release/2018-12/r/eclipse-ide-enterprise-java-developers
* Camunda Modeller
  https://camunda.com/download/modeler/

### Setup eclipse

* add server JBoss Community -> Wildfly (all required plugins are downloaded automatically)
* Link standard JRE to JDK1.8

## Servers

* Wildfly (latest)
  http://wildfly.org/downloads/
* Camunda BPM Wildfly Distribution
  https://camunda.org/release/camunda-bpm/wildfly10/7.10/

## Databases and dependencies

### Run H2 (tmp - will be replaced by an Docker environment)

Use the h2 jar file from `<WILDFLY_HOME>\modules\system\layers\base\com\h2database\h2\main` and copy it to a directory of your choice

	cd srv\db
	start java -jar h2-1.3.168.jar
	cd ..\..

### Docker depenencies

To run *mongo db*, *keycloak* (with database *postgres*) and *mysql* (to replace the h2 above in the future).
checkout `docks` project and go to `tp`(third party)

run

	docker-compose up -d

## Configure tech11 Insurance Platform product config (Capitol Insurance Limited)

	git clone git@bitbucket.org:techeleven/data-repo-capitol-versicherung.git

*in the following just named as directory `data-repo`*


## Configure Servers in eclipse

* Wildfly default setup (new server, ...) - link server to wildfly directory
<p align="center">
  <img src="your_relative_path_here" width="350" title="hover text">
  <img src="C:\Users\Houda\Pictures\Screenshots\server.png" width="350" alt="accessibility text">
</p>

* Camunda setup (new server, ...) - link server to camunda directory
** Change the Camunda server port: <CAMUNDA_HOME>\server\wildfly-10.1.0.Final\standalone\configuration\standalone.xml
 
	<socket-binding-group name="standard-sockets" default-interface="public" port-offset="${jboss.socket.binding.port-offset:-1000}">

   The port-offset is reduced for 1000 -> Camunda server is running on port 7080

** Add settings for some special user tasks from the BPM processes at the **Camunda standalone.xml**
   add system properties to standalone.xml

    <system-properties>
        <property name="CXC_PRINTING_DIR" value="C:\TMP/druckerstrasse"/>
    </system-properties>


** Add settings for the microservice at the **Wildfly standalone.xml**
   
    <system-properties>
        <property name="hero.root.dir" value="C:/Users/matthias/dev/hero"/>
        <property name="hero.repo.dir" value="${hero.root.dir}/data-repo"/>
        <property name="DOCS_TEMPLATE_DIR" value="${hero.repo.dir}/doc-templates"/>
        <property name="CALC_DIR" value="${hero.repo.dir}/product/calc"/>
        <property name="serviceRegistry.path" value="${hero.repo.dir}/service-registry.json"/>
        <property name="PRODUCT_DIR" value="${hero.repo.dir}/product"/>
        <property name="TARIFF_DIR" value="${hero.repo.dir}/product/tariffs"/>
        <property name="PARTNER_DIR" value="${hero.repo.dir}/partner"/>
        <property name="DOC_STORAGE_DIR" value="${hero.root.dir}/file-archive-system"/>
    </system-properties>    

** Add datasources for the microservices at the Wildfly standalone.xml
   Datasources section add:

		<datasource jndi-name="java:jboss/datasources/ExampleDS" pool-name="ExampleDS" enabled="true" use-java-context="true">
			<connection-url>jdbc:h2:mem:test;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE</connection-url>
			<driver>h2</driver>
			<security>
				<user-name>sa</user-name>
				<password>sa</password>
			</security>
		</datasource>
		<datasource jta="true" jndi-name="java:jboss/datasources/AccountingRecordsDS" pool-name="AccountingRecordsDS" enabled="true" use-java-context="true">
			<connection-url>jdbc:h2:tcp://localhost/C:/Users/matthias/dev/hero/srv/db/accounting-record</connection-url>
			<driver>h2</driver>
			<security>
				<user-name>sa</user-name>
				<password>sa</password>
			</security>
		</datasource>
		<datasource jta="true" jndi-name="java:jboss/datasources/ClaimDS" pool-name="ClaimDS" enabled="true" use-java-context="true">
			<connection-url>jdbc:h2:tcp://localhost/C:/Users/matthias/dev/hero/srv/db/hero-ng</connection-url>
			<driver>h2</driver>
			<security>
				<user-name>sa</user-name>
				<password>sa</password>
			</security>
		</datasource>
		<datasource jta="true" jndi-name="java:jboss/datasources/NumberGeneratorDS" pool-name="NumberGeneratorDS" enabled="true" use-java-context="true">
			<connection-url>jdbc:h2:tcp://localhost/C:/Users/matthias/dev/hero/srv/db/hero-ng</connection-url>
			<driver>h2</driver>
			<security>
				<user-name>sa</user-name>
				<password>sa</password>
			</security>
		</datasource>
		<datasource jta="true" jndi-name="java:jboss/datasources/JournalDS" pool-name="JournalDS" enabled="true" use-java-context="true">
			<connection-url>jdbc:h2:tcp://localhost/C:/Users/matthias/dev/hero/srv/db/hero-ng</connection-url>
			<driver>h2</driver>
			<security>
				<user-name>sa</user-name>
				<password>sa</password>
			</security>
		</datasource>


## Configure maven

* Change <USER_DIR>/.m2/settings.xml
* User the settings from SLACK channel and replace username and password


## Setup a project from BitBucket

* Checkout the git sources to a *SCM* folder with `scm\> git clone git@bitbucket.org:techeleven/policy.git`
* eclipse -> Import -> maven project (select scm folder)

## Test on CLI (to verify the setup)

* mvn clean package (should work)

Better use the scripts from the Jenkins pipeline

* docker-compose run --rm -w /app maven mvn clean package -DskipTests
* docker-compose up -d
* docker-compose exec -T -w /app maven mvn -pl server verify -Djacoco.address=app

## Run in eclipse

* Add project (*policy*) to server
* Start server

## Test service

just enter into the browser `http://localhost:8080/policy/api/products` and see if you get a result
*portfolio* is the old name for the policy module (have to be renamed)

