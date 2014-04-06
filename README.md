## OpenShift Apache Solr 4.7.1 Quickstart

This is an OpenShift Quickstart repository to help you get Apache Solr 4.7.1 up and running quickly.

### Installation

To install the quick start use the following commands

    # Create your application to host your Apache Solr instance using jbossews cartridge
    rhc app create solr jbossews-2.0
    
    # Remove build material
    git rm -rf src/ pom.xml
    git commit -a -m "Removing default files"
    
    # Pull in quickstart
    git remote add upstream -m master https://github.com/Categorize/openshift-solr-quickstart.git
    git pull -s recursive -X theirs upstream master
    
    # Customise and then commit changes
    git commit -am "Added Solr Quickstart"
    git push

### What Was Done

Using the quick start an Apache Solr instance is created using the example collection found within the binary distribution of Apache Solr.

### Usage

Having pushed the updated code you should find the Solr Admin URL on:

    http://solr-<domainname>.rhcloud.com/

Before using the Solr instance for development you will need to customise the configuration and schema. To do this you need to adjust the [solrconfig.xml](http://wiki.apache.org/solr/SolrConfigXml) and [schema.xml](http://wiki.apache.org/solr/SchemaXml) within solr.home based on your needs.

### Support

This quick start is provided provided "as is", with absolutely no warranty expressed or implied. Any use is at your own risk.
