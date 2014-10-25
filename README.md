## OpenShift Apache Solr 4.10.1 Quickstart

This is an OpenShift Quickstart repository to help you get Apache Solr 4.10.1 up and running quickly.

### Installation

To install the quick start use the following commands

    # Create your application to host your Apache Solr instance using jbossews cartridge
    rhc app create solr jbossews-2.0
    
    # Remove build material
    git rm -rf src/ pom.xml
    git commit -a -m "Removing default files"
    
    # Pull in quickstart
    git remote add upstream -m master https://github.com/LogicalSpark/openshift-solr-quickstart.git
    git pull -s recursive -X theirs upstream master
    
    # Edit tomcat-users.xml and web.xml (see below)
    # Edit schema.xml and solrconfig.xml in the solr.home/collection1/conf/ folder
    # Any additional customization and then commit changes
    git commit -am "Added Solr Quickstart"
    git push

### Tomcat Security
Edit .openshift/conf/tomcat-users.xml. Replace everything within the ``` <tomcat-user>``` element with (using your own username and password) and save:

```
  <role rolename="manager-gui"/>
  <role rolename="solr_admin"/>
  <user username="userxxxx" password="passwordxxx" roles="manager-gui,solr_admin"/>
```
### Optional Solr Security
Edit web.xml by and going to .openshift/conf/web.xml
Add the following lines within the ```<web-app>``` element and save the war file:

```
  <security-constraint>
    <web-resource-collection>
      <web-resource-name>Solr Lockdown</web-resource-name>
      <url-pattern>/</url-pattern>
    </web-resource-collection>
    <auth-constraint>
      <role-name>solr_admin</role-name>
      <role-name>admin</role-name>
    </auth-constraint>
  </security-constraint>
  <login-config>
    <auth-method>BASIC</auth-method>
    <realm-name>Solr</realm-name>
  </login-config> 
```
### What Was Done

Using the quick start an Apache Solr instance is created using the example collection found within the binary distribution of Apache Solr.

### Usage

Having pushed the updated code you should find the Solr Admin URL on:

    http://solr-<domainname>.rhcloud.com/

Before using the Solr instance for development you will need to customise the configuration and schema. To do this you need to adjust the [solrconfig.xml](http://wiki.apache.org/solr/SolrConfigXml) and [schema.xml](http://wiki.apache.org/solr/SchemaXml) within solr.home based on your needs.

### Support

This quick start is provided provided "as is", with absolutely no warranty expressed or implied. Any use is at your own risk.
