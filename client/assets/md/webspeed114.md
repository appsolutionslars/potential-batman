# whoGloo Inc. (www.whogloo.com)
Requirements for using quay.io/whogloo/webspeed114 image: 

## Properties directory 
Properties directory with webspeed.properties file to merge into the /usr/openedge114/ubroker.properties file 
    e.g. -v /opt/app/properties:/opt/properties

## Config file for WebSpeed
Depending on the setup for WebSpeed, there may be a need for an /opt/config directory with a .pf file (e.g. /opt/config/ws_sportsgloo.pf) for the webspeed broker. 
    e.g. -v /opt/config/ws_sportsgloo.pf:/opt/config/ws_sportsgloo.pf  
   
## Application directories referenced in PROPATH
if the WebSpeed broker references directories in the PROPATH, they need to be available from mapped volumes or from mapped directories
    e.g. 
```    
-v /opt/apps/development/sportsgloo:/opt/apps/sportsgloo 
-v /opt/apps/development/codeglooruntime:/opt/apps/codeglooruntime 
-v /opt/apps/development/stomp:/opt/apps/stomp
```

## Standar startup - CMD ["supervisord", "-c", "/etc/supervisor.conf"]
If the image is not started with any command line parameters to execute, then it will by default start a "supervisord" daaemon using the built in startup script
`CMD ["supervisord", "-c", "/etc/supervisor.conf"]`. 

This will pick up any *.sv.conf files in the `/etc/supervisor/conf.d` directory and execute this when it starts. 

The default processes for the webspeed 114 images are:
``` 
[program:proadsv]
command=/bin/bash -c "proadsv -start"
redirect_stderr=true
```

```
[program:apache2]
command=/bin/bash -c "/etc/init.d/apache2 start"
redirect_stderr=true
```
## Running webspeed114 image

The following are sample command lines to start webspeed114:

Run with a bash shell that does not start any of the background processes:                   
```
docker run -it -p 8081:80 -p 9099:9098 -v /opt/docker/docker_nodegloo/webspeed114/properties/webspeed.properties:/opt/properties/webspeed.properties -v /opt/docker/docker_nodegloo/webspeed114/config:/opt/config -v /opt/apps/development/sportsgloo:/opt/apps/sportsgloo -v /opt/apps/development/codeglooruntime:/opt/apps/codeglooruntime -v /opt/apps/development/stomp:/opt/apps/stomp quay.io/whogloo/webspeed114 /bin/bash
```

Run with a default setting, starting the OE Admin Server and Apache server. This will not start any WebSpeed brokers, as none are defined in the ubroker.properties file by default.                   
```
docker run -it -p 8081:80 -p 9099:9098 -v /opt/docker/docker_nodegloo/webspeed114/properties/webspeed.properties:/opt/properties/webspeed.properties -v /opt/docker/docker_nodegloo/webspeed114/config:/opt/config -v /opt/apps/development/sportsgloo:/opt/apps/sportsgloo -v /opt/apps/development/codeglooruntime:/opt/apps/codeglooruntime -v /opt/apps/development/stomp:/opt/apps/stomp quay.io/whogloo/webspeed114
```

Run with a default setting, starting the OE Admin Server and Apache server. This will not start any WebSpeed brokers, as none are defined in the ubroker.properties file by default.                   
```
docker run -it -p 8081:80 -p 9099:9098 -v /opt/docker/docker_nodegloo/webspeed114/properties/webspeed.properties:/opt/properties/webspeed.properties -v /opt/docker/docker_nodegloo/webspeed114/config:/opt/config -v /opt/apps/development/sportsgloo:/opt/apps/sportsgloo -v /opt/apps/development/codeglooruntime:/opt/apps/codeglooruntime -v /opt/apps/development/stomp:/opt/apps/stomp quay.io/whogloo/webspeed114
```  
