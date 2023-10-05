# Apache Web Server - introduction and basic configuration

## What is Apache Web Server?
Apache is a free and open-source web server that delivers web content through the internet.

Apache functions as a way to communicate over networks from client to server using the TCP/IP protocol. Apache can be used for a wide variety of protocols, but the most common is HTTP/S. HTTP/S or Hyper Text Transfer Protocol (S stands for Secure) is one of the main protocols on the web, and the one protocol Apache is most known for.

HTTP/S is used to define how messages are formatted and transmitted across the web, with instructions for browsers and servers on how to respond to various requests and commands. Hypertext Transfer Protocol Secure is usually through port 443 with the unsecured protocol being through port 80.

The Apache server is configured via config files in which modules are used to control its behavior. By default, Apache listens to the IP addresses configured in its config files that are being requested. This is where one of Apaches many strengths come into play.

### Features of Apache Web Server:
- Handling of static files
- Loadable dynamic modules
- Auto-indexing
- Compatible with IPv6
- Supports HTTP/2
- FTP connections
- Gzip compression and decompression
- Bandwidth throttling
- Perl, PHP, Lua scripts
- Load balancing
- Session tracking
- URL rewriting
- Geolocation based on IP address
- Multi platform - Linux, Windows, Mac (The only difference would be directory paths and installation processes)

## Directives
Apache directives are a set of rules which define how your server should run, the number of clients that can access your server, etc. you can configure them by using the apache2.conf or httpd.conf files.

Here is a list of the available directives in the [official Apache documentation](https://httpd.apache.org/docs/2.4/mod/directives.html).

Some of the most used directives are:

### Server Name
The ServerName directive is used to define or set the name of your domain name or sub-domains.

The ServerName directive is optional and specifies what FQDN your site should answer to. The default virtual host has no ServerName directive specified, so it will respond to all requests that do not match a ServerName directive in another virtual host.

### Listen
Listen is the directive used to define the port Apache listens on and also any specific IP address to listen on. If the IP address is not specified, Apache2 will listen to all IP addresses assigned to the machine it runs on.

By default, Apache listens on port 80, but you can define this to a nonstandard port if needed. You can also use Listen to define specific addresses that the server will accept connections from.

### LoadModule
LoadModule is the directive used to inform the Apache server of a module to be loaded. A list with available modules can usually be found in the mods-available directory.

### ServerRoot
The ServerRoot directive sets the directory in which all the webserver's global configurations are defined and set.

Typically it will contain the subdirectories conf/ and logs/. Relative paths in other configuration directives (such as Include or LoadModule, for example) are taken as relative to this directory.

In Debian and Ubuntu it is /etc/apache2 and in RHEL-based distributions it is /etc/httpd. That’s where all the configuration for virtual hosts, modules, ports, envvars, etc. lives.

### DocumentRoot
The DocumentRoot directive specifies where Apache2 should look for the files that are requested by the clients and the files which should be rendered and processed by the webserver. This is the directory from which Apache will read the contents that the visitor will access over the browser. Or in other words, this is the directory that forms the tree of directories that will be accessible over the web.
The "DocumentRoot" option specifies where the content that is requested for this Virtual Host will be located.

The default value is /var/www/html, as specified in /etc/apache2/sites-available/000-default.conf.

### Include
This directive allows inclusion of other configuration files from within the server configuration files. This is very useful when you want to give access to the configuration of a website to a developer team or vendor employee, whithout giving them root access (becasue /etc requires root).

## .htaccess file
An .htaccess file is used for an Apache web server as a way to configure the details of your website without altering the server configuration files. This file begins with a period to signify that it’s hidden within the folder. An .htaccess file can be used to load customized error pages (such as 404 pages), create URL redirects, implement password-protected authentication for specific directories on your server, and more.

It is not advised however to use .htaccess anymore. The following is a quote from the [official Apache documentation of the .htaccess file](https://httpd.apache.org/docs/2.4/howto/htaccess.html):

> You should avoid using .htaccess files completely if you have access to httpd main server config file. Using .htaccess files slows down your Apache http server. Any directive that you can include in a .htaccess file is better set in a Directory block, as it will have the same effect with better performance.

## Virtual Hosts
Virtuals hosts allow a single server to host multiple websites or web applications. Each virtual host has its own separate configuration, allowing different domains or subdomains to be served independently. Virtual hosts are a crucial feature for efficiently managing and hosting multiple websites on a single server.

### Name-based
This is the most common type of virtual hosting. It relies on the HTTP Host header sent by the client's browser to determine which virtual host configuration to use. Multiple domains can share the same IP address, as long as they have different domain names.

### IP-based
Each virtual host has its own unique IP address. This method is less common and may be used when strict separation of websites is required, or when using older web browsers that don't support the Host header.

### Port-based
In this approach we use the same IP address and hostname, but the webistes listen on different ports.

## Starting the port-based demo
Run `docker-compose up -d` to start the demo. You can then open [localhost:8081](http://localhost:8081), [localhost:8082](http://localhost:8082) and/or [localhost:8083](http://localhost:8083) to see the port-based virtual hosts working. You can also play with the configuration in /conf and /www directories and the docker-compose file.
