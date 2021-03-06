---
group: installation-guide
title: Magento 2.4 technology stack requirements
functional_areas:
  - Install
  - System
  - Setup
---

## Operating systems (Linux x86-64)

Linux distributions, such as RedHat Enterprise Linux (RHEL), CentOS, Ubuntu, Debian, and similar.
Magento is not supported on:

*  Windows OS
*  Mac OS

## Memory requirement

Upgrading the Magento applications and extensions you obtain from Magento Marketplaces and other sources can require up to 2GB of RAM. If you are using a system with less than 2GB of RAM, we recommend you create a [swap file](https://support.magento.com/hc/en-us/articles/360032980432); otherwise, your upgrade might fail.

## Composer (latest stable version)

[Composer][] is required for developers who wish to contribute to the Magento 2 codebase or anyone who wishes to develop Magento extensions.

## Web servers

*  [Apache 2.4][]

   In addition, you must enable the Apache `mod_rewrite` and `mod_version` modules. The [`mod_rewrite`][] module enables the server to perform URL rewriting. The [`mod_version`][] module provides flexible version checking for different `httpd` versions. For more information, see [our Apache documentation][].

*  [nginx 1.x][]

## Database

*  MySQL 8.0 for on-premise installations
*  MariaDB 10.4 for {{site.data.var.ece}} projects

Magento is also compatible, but has not been tested and is not recommended, with MySQL 5.7.9, MariaDB 10.2, and Percona 5.7.

{:.bs-callout-info}
Magento only uses MySQL features compatible with MariaDB. MariaDB may not be compatible with all MySQL features, however, so be sure to research compatibility issues before using a feature in your Magento module.

## PHP

*  ~7.4.0

Magento 2.4.0 can be installed with 7.3, but it is not tested or recommended. It is intended for upgrading from Magento 2.3.x to Magento 2.4.0.

{:.bs-callout-warning}
There is a [bug](https://bugs.php.net/bug.php?id=79174) in PHP 7.4.2 which causes some messages to not render properly. Magento recommends using other versions of 7.4.

### Required PHP extensions

{:.bs-callout-info}
The [PHP installation instructions][] include a step for installing these extensions.

<!--{% assign platform-req = site.data.codebase.v2_4.open-source.composer_lock.platform %}-->
{% include install/php-extensions-template.md %}

Refer to [official PHP documentation][] for installation details.

### PHP OPcache

We strongly recommend you verify that [PHP OPcache][] is enabled for performance reasons. The OPcache is enabled in many PHP distributions. To verify if it is installed, see our [PHP documentation][].

If you must install it separately, see the [PHP OPcache documentation][].

### PHP settings

We recommend particular PHP configuration settings, such as `memory_limit`, that can avoid common problems when using Magento.

For more information, see [Required PHP settings][].

## Elasticsearch

As of Magento 2.4.0, MySQL is no longer used for search. You must use [Elasticsearch]({{page.baseurl}}/install-gde/prereq/elasticsearch.html). Magento supports Elasticsearch 7.6.x.

{:.bs-callout-warning}
Magento no longer supports Elasticsearch [2.x, 5.x, and 6.x][].

## SSL

*  A valid [security certificate][] is required for HTTPS.
*  Self-signed SSL certificates are not supported.
*  Transport Layer Security (TLS) requirement - PayPal and `repo.magento.com` both require TLS 1.2 or later:

   *  [More information about PayPal][]

### Required system dependencies

Magento requires the following system tools for some of its operations:

*  [bash][]
*  [gzip][]
*  [lsof][]
*  [mysql][]
*  [mysqldump][]
*  [nice][]
*  [php][]
*  [sed][]
*  [tar][]

### Mail server

Mail Transfer Agent (MTA) or an SMTP server

## Technologies Magento can use

*  [Redis][] version 5.0 is recommended and used in testing for page caching and session storage
*  [Varnish]({{page.baseurl}}/config-guide/varnish/config-varnish.html) version 6.x (tested with 6.3.1)

*  RabbitMQ 3.8.x

   [RabbitMQ][]{:target="_blank"} can be used to publish messages to queue and to define the consumers that receive the messages asynchronously.

### {{site.data.var.ee}} only

*  Three master databases

   These [master databases][] provide scalability advantages for different functional areas of the Magento application such as checkout, orders, and all remaining Magento2 application tables.

### Optional but recommended

*  [php_xdebug 2.5.x][]{:target="_blank"} or later (development environments only; can have an adverse effect on performance)

{:.bs-callout-info}
There is a known issue with `xdebug` that can affect Magento installations or access to the storefront or Magento Admin after installation. For details, see [Known issue with xdebug][].

*  PHPUnit (as a command-line tool) 9.0.0

<!-- Link Definitions -->
[`mcrypt`]: http://php.net/manual/en/book.mcrypt.php
[Known issue with xdebug]: https://support.magento.com/hc/en-us/articles/360034242212
[php_xdebug 2.5.x]: http://xdebug.org/download.php
[master databases]: {{page.baseurl}}/config-guide/multi-master/multi-master.html
[bash]: https://www.gnu.org/software/bash/
[gzip]: https://www.gzip.org/
[lsof]: https://linux.die.net/man/8/lsof
[mysql]: https://www.mysql.com/
[mysqldump]: https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html
[nice]: https://linux.die.net/man/1/nice
[php]: http://www.php.net/
[sed]: https://www.gnu.org/software/sed/manual/sed.html
[tar]: https://linux.die.net/man/1/tar
[Composer]: https://glossary.magento.com/composer
[Apache 2.4]: http://httpd.apache.org/download.cgi
[`mod_rewrite`]: https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html
[`mod_version`]: https://httpd.apache.org/docs/2.4/mod/mod_version.html
[our Apache documentation]: {{page.baseurl}}/install-gde/prereq/apache.html
[nginx 1.x]: https://nginx.org/en/download.html
[ZenHub board]: https://app.zenhub.com/workspace/o/magento-engcom/php-7.2-support/boards?repos=116423356,116426364,115111902
[PHP installation instructions]: prereq/php-settings.html
[official PHP documentation]: http://php.net/manual/en/extensions.php
[PHP OPcache]: http://php.net/manual/en/intro.opcache.php
[PHP documentation]: prereq/php-settings.html
[PHP OPcache documentation]: http://php.net/manual/en/opcache.setup.php
[Required PHP settings]: {{ page.baseurl }}/install-gde/prereq/php-settings.html
[security certificate]: https://glossary.magento.com/security-certificate
[More information about PayPal]: {{page.baseurl}}/install-gde/system-requirements_tls1-2.html
[Redis]: {{page.baseurl}}/config-guide/redis/config-redis.html
[Varnish]: {{page.baseurl}}/config-guide/varnish/config-varnish.html
[Elasticsearch]: {{page.baseurl}}/install-gde/prereq/elasticsearch.html
[2.x, 5.x, and 6.x]: https://www.elastic.co/support/eol
[RabbitMQ]: {{page.baseurl}}/config-guide/mq/rabbitmq-overview.html
