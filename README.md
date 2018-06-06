# Collaboration-System-Event-Logs

<p>
Event logging module is a part of the Collaboration system. This module deals with the logging of the user interaction events, such as view an article.
This module works as a middleware in Django project and captures and filters the request based on the specification.
</p>

## Setup

<p>To setup this module with the Collaboration system, perform the follwing steps:</p>
1. copy the 'eventlog' folder into the root of the main Django project.
2. go to project's `settings.py` and in the set of the middlewares add following line:

```python
MIDDLE_WARE = [
...
'evenlog.middleware.Middleware'
]
```

And, thats all, you are done!

## Setting up ELK Stack with docker

1. Place elasticsearch, logstash, kibana folders of evelog-Docker in the Collaboration-System repository.

2. Replace the docker-compose.yml file of Collaboration-System repository with the evelog-Docker's docker-compose.yml.

3. Go to `eventlog/main/settings.py` and change address and port as follows:
```python
SERVER_CONF = {
		...,
		"address": "logstash",
                "port": 5000,
		...,
}
```
4. Run the following commands inside the Collaboration-System repository:
```
   docker-compose build
   docker-compose up
```

### Configuring the proxy

1. To setup proxy go to `eventlog/main/settings.py` 
2. For `SERVER_CONF` set `'use_proxy' = True`.
3. Specify the proxy configuration as follows:
```python
SERVER_CONF = {
		...,

              "proxies": {
                    "http": "http://proxy.cse.iitb.ac.in:80",
                    "https": "https://proxy.cse.iitb.ac.in:80",
                    "ftp": "ftp://proxy.cse.iitb.ac.in:80",
              }
}
```
4. To add authentication for proxy add follwowing to `SERVER_CONF` else remove it:
```python
SERVER_CONF = {
		...,
		"proxy_auth": {
                         "username": "<your-proxy-authentication-name>",
                         "password": "<your-proxy-authentication-password>"
                }
	
}

```

##  Debugging and Logging

Debugging module is defined in utils.py and enables 5 levels of logging along with some color customizations for better viewing.

1. To enable debugging go to `eventlog/main/settings.py`.
2. Set `DEBUG = True`




