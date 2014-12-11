# whoGloo Inc. (www.whogloo.com)
## Image: openedge114db

## Purpose for this image
Progress 11.4 only database installed.

## Standar startup - CMD ["supervisord", "-c", "/etc/supervisor.conf"]
If the image is not started with any command line parameters to execute, then it will by default start a "supervisord" daaemon using the built in startup script
`CMD ["supervisord", "-c", "/etc/supervisor.conf"]`. 

This will pick up any *.sv.conf files in the `/etc/supervisor/conf.d` directory and execute this when it starts. 

No supervisor script is configured for this image

## Running openedge114db image

The following are sample command lines to start database114:

Run with a bash shell that does not start any of the background processes:                   
```
docker run -ti -p 9090:9090 quay.io/whogloo/openedge114db /bin/bash
```

For the configuration of the Progress Explore service, you will need to expose port 9090 internal. Expose externally anything. 
Setting environment variables for default setting, use /usr/sbin/setdlc114.sh and start Progress Admin service
```
. setdlc114.sh
proadsv -start
```

Complet the configuration from http://[container ip]:9090 
User: ‘admin’. Password: ‘progress’.
