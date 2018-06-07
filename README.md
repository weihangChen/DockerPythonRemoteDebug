# DockerPythonRemoteDebug



I have been trying to make remote debugging with ptvsd work by following this [tutorial](https://docs.microsoft.com/en-us/visualstudio/python/debugging-python-code-on-remote-linux-machines). My personal goal is to put all python libraries in a running container, then do remote debug against the docker container as for local development. Here is the [video](https://youtu.be/zZiwSvRuUyE)


There has been problems getting it to work, the main problem is that visual studio version needs to match up the ptvsd tool. In my case, my VS version is **15.7.2** and only ptvsd **3.2.1** works well with that. Here is the [discussion](https://github.com/Microsoft/PTVS/issues/4270#issuecomment-392965960) that makes it work.

the only docker command you need to get it running is 
```
docker-compose run --rm -p 5678:5678 dockerremotedebug
```

the command above does not run the python script in the dockerfile, you need to spin up another terminal and 
```
docker exec -it your-container-id bash
```

then manually start the python script

```
python test.py
```
now attach to ```tcp://my_secret@127.0.0.1:5678/``` in your hoste machine.

