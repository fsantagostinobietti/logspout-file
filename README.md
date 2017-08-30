# logspout-file builder
Project used to build docker image for [logspout](https://github.com/gliderlabs/logspout) with [logspout-file module](https://github.com/fsantagostinobietti/logspout-file) built in.

Implementation is based on instruction in https://github.com/gliderlabs/logspout/tree/master/custom.

 
## build docker image
```
$ docker build -t logspout-file:latest .
```

## usage example
```
# start 'logspout-file' instance 
$ docker run -d --name="logspout-file" --volume=/var/run/docker.sock:/var/run/docker.sock -v $(pwd)/log:/var/log logspout-file:latest file://filename.log?maxfilesize=10240

# start applications you want to collect logs
$ docker run ...
```

If your applications produce log lines you'll see them in mounted volume (in this example '$(pwd)/log').
```
$ la -1 $(pwd)/log
filename.log
filename.log.2017-08-29T11:49:12Z
```

## custum options
You can customize some features using options:

option |  description   | default value
---------|----------------|--------------
maxfilesize | max size of rotated file | 100 Mbyte
