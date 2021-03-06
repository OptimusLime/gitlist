# GitList: an elegant and modern git repository viewer
[![Build Status](https://secure.travis-ci.org/klaussilveira/gitlist.png)](http://travis-ci.org/klaussilveira/gitlist)

GitList is an elegant and modern web interface for interacting with multiple git repositories. It allows you to browse repositories using your favorite browser, viewing files under different revisions, commit history, diffs. It also generates RSS feeds for each repository, allowing you to stay up-to-date with the latest changes anytime, anywhere. GitList was written in PHP, on top of the [Silex](http://silex.sensiolabs.org/) microframework and powered by the Twig template engine. This means that GitList is easy to install and easy to customize. Also, the GitList gorgeous interface was made possible due to [Bootstrap](http://twitter.github.com/bootstrap/). 

## Features
* Multiple repository support
* Multiple branch support
* Multiple tag support
* Commit history, blame, diff
* RSS feeds
* Syntax highlighting
* Repository statistics

## Screenshots
[![GitList Screenshot](http://dl.dropbox.com/u/62064441/th1.jpg)](http://cloud.github.com/downloads/klaussilveira/gitlist/1.jpg)
[![GitList Screenshot](http://dl.dropbox.com/u/62064441/th2.jpg)](http://cloud.github.com/downloads/klaussilveira/gitlist/2.jpg)
[![GitList Screenshot](http://dl.dropbox.com/u/62064441/th3.jpg)](http://cloud.github.com/downloads/klaussilveira/gitlist/3.jpg)
[![GitList Screenshot](http://dl.dropbox.com/u/62064441/th4.jpg)](http://cloud.github.com/downloads/klaussilveira/gitlist/4.jpg)
[![GitList Screenshot](http://dl.dropbox.com/u/62064441/th5.jpg)](http://cloud.github.com/downloads/klaussilveira/gitlist/5.jpg)

You can also see a live demo [here](http://git.gofedora.com).

## Authors and contributors
* [Klaus Silveira](http://www.klaussilveira.com) (Creator, developer)

## License
[New BSD license](http://www.opensource.org/licenses/bsd-license.php)

## Todo
* improve the current test code coverage
* test the interface
* error handling can be greatly improved during parsing
* submodule support
* multilanguage support

## Requirements
In order to run GitList on your server, you'll need:

* git
* Apache and mod_rewrite enabled
* PHP 5.3.3




## Installing
Download the GitList latest package and decompress to your `/var/www/gitlist` folder, or anywhere else you want to place GitList. You can also clone the repository:

```
git clone https://github.com/klaussilveira/gitlist.git /var/www/gitlist
```

Rename the `config.ini-example` file to `config.ini`. Now open up the `config.ini` and configure your installation. You'll have to provide where your repositories are located and the base GitList URL (in our case, http://localhost/gitlist or in the cloud: http://[amazon elastic ip address]/gitlist). Now, let's create the cache folder and give the correct permissions:



#Cloud based installation:

I grabbed an Ubuntu 11.04 Community AMI (with Node installed I think -- for playing around later)
ami-2f3dfb46
Launch the instance 

ssh into the ec2 instance,  user = ubuntu@[amazon provided address or elastic IP]

```
sudo apt-get update
sudo apt-get install git php5 apache2
```
this installed git, php and apache, pretty much everything you need
but you need to enable mod_write for apache

```
sudo a2enmod rewrite
```

restart apache to have rewrite module enabled

```
sudo /etc/init.d/apache2 restart
```


boom, updated
Now, I wanted to make the website's main directory redirect to the gitlist subdirectory so how do we do this? Well, we need a .htaccess file inside of our document root (/var/www/ by default)
I will assume it's at /var/www

```
cd /var/www
sudo vim .htaccess
```

this should read:
```
<IfModule mod_rewrite.c>
    Options +FollowSymlinks

RewriteEngine On
RewriteCond %{REQUEST_URI} !^/gitlist/index.php
RewriteCond %{REMOTE_HOST} !^123\.456\.789
RewriteCond %{REQUEST_URI} !^/gitlist/?
RewriteCond %{REQUEST_URI} /(.*)$
RewriteRule (.*) /gitlist/index.php [R=301,L]

</IfModule>
```
And that's it. What you can see is that it will redirect any request coming in to our gitlist/index.php.

This means http://yourdomain.com/ => is accessing /var/www/gitlist/index.php

This also means, http://yourdomain.com/typingnothingohmygod will redirect to /var/www/gitlist/index.php

And that's really all I did differently to get this hosted on an amazon ec2 instance

follow these other instructions...


```
cd /var/www/gitlist
mkdir cache
chmod 777 cache
```

That's it, installation complete! If you're having problems, check this [tutorial](http://gofedora.com/insanely-awesome-web-interface-git-repos/) by Kulbir Saini or the [Troubleshooting](https://github.com/klaussilveira/gitlist/wiki/Troubleshooting) page.

## Further information
If you want to know more about customizing GitList, check the [Customization](https://github.com/klaussilveira/gitlist/wiki/Customizing) page on the wiki. Also, if you're having problems with GitList, check the [Troubleshooting](https://github.com/klaussilveira/gitlist/wiki/Troubleshooting) page. Don't forget to report issues and suggest new features! :)
