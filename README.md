# Description #

A cookbook for Opscodes Chef open-source systems integration framework to install and configure the neo4j Server and Web-Interface.

neo4j is an open source log management solution that stores your logs in ElasticSearch. It consists of a server written in Java that accepts your syslog messages via TCP, UDP or AMQP and stores it in the database. The second part is a web interface that allows you to manage the log messages from your web browser.

http://www.neo4j.org

# Requirements #

## Platform ##
The Cookbooks is build for the following platforms:
* Debian, Ubuntu
* CentOS, Red Hat

The Cookbooks is tested on the following platforms:
* Debian 6.05
* Ubuntu 10.04-4, 12.04
* CentOS 5.8, 6.2

## Cookbooks ##
To install the coockbook use the following commands, depending to your platform:

    gem install librarian
    cd chef-repo
    librarian-chef init

    cat >> Cheffile <<END_OF_CHEFFILE
    cookbook 'apt', :git => 'https://github.com/opscode-cookbooks/apt.git'
    cookbook 'yum', :git => 'https://github.com/opscode-cookbooks/yum.git'
    cookbook 'java', :git => 'https://github.com/opscode-cookbooks/java.git'
    cookbook 'neo4j', :git => 'https://github.com/sebwendel/chef-neo4j.git'
    END_OF_CHEFFILE

    librarian-chef install

    knife cookbook upload apt yum java neo4j

# Recipes #
The cookbock provides the following recipes:
* `recipe[neo4j]` - Deploye the neo4j server and web-interface.
* `recipe[neo4j::server]` - Just deploye the neo4j server.

This will install the java dependencie, the neo4j server and the declared plugins.

# Attributes #
The Cookbook comes with a bunch of attributes the following are the the most important. All attributes work out of the box but can be overridden.
## Version ##
* `default['neo4j']['server_version']` - Specify the server version you want to install, default is "0.9.6p1".

## EMail ##
* `default['neo4j']['email_host']` - Specify the mail server to send the reports, default is "127.0.0.1".
* `default['neo4j']['email_port']` - Specify the mail servers port, default is "25".
* `default['neo4j']['email_auth']` - Specify the mail merver authentication protocol, default is "plain".
* `default['neo4j']['email_user']` - Specify the mail server user for authentication, default is "nil".
* `default['neo4j']['email_passwd']` - Specify the mail server password for authentication, default is "nil".
* `default['neo4j']['email_address']` - Specify the senders mail address, default is "neo4j@#{node['fqdn']}".
* `default['neo4j']['email_domain']` - Specify the senders mail domain, default is "127.0.0.1".

## Reports ##
* `default['neo4j']['stream_alarms_cron_minute']` - Specify the cron cycle to send alarm, default is 15 minutes.
* `default['neo4j']['stream_subscriptions_cron_minute']` - Specify the cron cycle to send subscriptions, default is 15 minutes.

For a better understanding of which configuration parameters are available have a look in the default attributes file.

# Usage #
1. download and install all dependencies
1. override the attributes if necessary
1. check all interface, port and authentication config
1. add the recipe to your nodes runlist


    {
      "run_list": [
        "recipe[neo4j]"
      ]
    }

If you use all dependencies from the described sources the cookbook should work out of the box without any changes of attributes.

# Limitations and Issues #
If you have any questions or recommendations just create a issue at the github repository.
If you want to help have a lock at the github issues section, patches are more than welcome.

* For now there is no authentication on the backend side.
* All dependencies will be automatically installed and cannot be define alternatively.

# License and Author #

Author: Sebastian Wendel, (<packages@sourceindex.de>)

Copyright: 2012, SourceIndex IT-Serives

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

![Tracking Pixel](https://tracking.sourceindex.de/piwik.php?idsite=5&amp;rec=1)
