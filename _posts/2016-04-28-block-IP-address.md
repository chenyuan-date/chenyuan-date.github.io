---
layout: post
title: Use .htaccess to limit IP address 
author: CY
description: "A method to limit IP address via .htaccess"
tags: [Linux]
categories: [Linux]
share: false
image:
  background: triangular.png
---

Sometimes, in order to avoid so many useless visit to your server, which may cause a waste of resource and slow response, it is necessary to limit IP address.

Create a file named .htaccess in the web directory, then add the following contents according to your purpose.

## Block IP address  

### Block certain IP address

```
order allow,deny
deny from 222.222.222.222
allow from all
```

### Block several IP addresses, just several deny from will be OK

```
order allow,deny
deny from 222.222.222.222
deny from 111.111.111.111
deny from ***.***.***.***
allow from all
```

### Block one entire IP period 

```
order allow,deny
deny from 222.222.222
allow from all
```

### Block part of one entire IP period

```
order allow,deny
deny from 222.222.222.100/200
allow from all
```

## Allow IP address 

### Allow certain IP address

```
order allow,deny
allow from 222.222.222.222
deny from all
```

### Allow several IP addresses, just several allow from will be OK

```
order allow,deny
allow from 222.222.222.222
allow from 111.111.111.111
allow from ***.***.***.***
deny from all
```

### Allow one entire IP period 

```
order allow,deny
allow from 222.222.222
deny from all
```

### Allow part of one entire IP period

```
order allow,deny
allow from 222.222.222.100/200
deny from all
```

## Block certain website

If you find some websites copy your blog, just block them!

```
order allow,deny
deny from .copy.com [this is website]
allow from all
```

This will block the visit from copy.com website, there is a dot before copy.com, this will block all its website (including second-level domain).



## Reference        

[.htaccess根据IP地址限制访问](http://www.sjyhome.com/htaccess/limit-the-ip-address.html) 