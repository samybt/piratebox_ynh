# PirateBox
## Overview

**Warning: work in progress**

PirateBox app for [YunoHost](http://yunohost.org/).

Based on [php-piratebox](https://github.com/jvaubourg/php-piratebox).

## Features

* Open wifi Access Point (AP)
* Once connected to the AP, you can go on *http://pirate.box*, or *http://www.google.com* or even *http://lqksjdhfkljhsdf.qsdf* (or let your captive portal detection mechanism do its job)
* All destinations lead to the PirateBox web page
* No authentication required for uploading, downloading or deleting (lawless zone)
* Of course, works without internet connection
* [Screenshot (app)](https://raw.githubusercontent.com/labriqueinternet/piratebox_ynh/master/screenshot_app.png), [screenshot (admin)](https://raw.githubusercontent.com/labriqueinternet/piratebox_ynh/master/screenshot_admin.png)
* [Web interface features](https://github.com/jvaubourg/php-piratebox) and [more screenshots](https://github.com/jvaubourg/php-piratebox#screenshots)

The YunoHost administration is only available through the wired connection.

## How It Works ##

Explanations:

1. all packets to port 53 are redirected to the port 4253,
2. a fake DNS resolver listens on the port 4253, and systematically responds the IPv4 address of the server (a fake DNS resolver is mandatory for responding to any requests, without internet connection),
3. a MASQUERADE rule allows the fake DNS to respond in place of the initially requested resolver,
4. all packets to port 80 are redirected to the port 4280,
5. a Nginx vhost listens on the port 4280, and redirects to the PirateBox web page.

## Prerequisites

* Debian Jessie
* YunoHost >= 2.2.0
* [Hotspot app for YunoHost](https://github.com/jvaubourg/hotspot_ynh)

## Limitations ##

* IPv4-only because the NAT table is not available for IPv6 before the kernel 3.9.0 and iptables 1.4.18 (not in Debian stable for now)
* Don't redirect to the PirateBox web page with explicit HTTPS requests (in order to avoid offering self-signed certificates on well-known domains)
