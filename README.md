socker
======

Dockerised Jupyter (ipython) Notebook for statistical genetics and genomics.
Customisable, reproducible  and disposable environment for authoring genetic analysis documents.

For info about ipython scipystack see http://odewahn.github.io/docker-jumpstart/ipython-notebook.html

Provides
--------

- IPython notebook, SciPy stack
- VCFtools
- VCFLib
- Samtools/HTSLib
- BedTools
- R base (using Rocker)
- R data manipulation and genetics tools
- iPython Rkernel and R2py magic

To Run
------

- On OSX or Windows, install [Boot2Docker](https://github.com/boot2docker/boot2docker)
- or [docker-machine](https://docs.docker.com/machine/)
- Start up Boot2docker

```
boot2docker up
$(boot2docker shellinit) ## on OSX or Linux
```
- see
- Get daemon running
```
sudo /etc/init.d/docker start
```

- Configure docker when behind a proxy

(Check to see if profile file exists and add the needed configuration)
```
vi /var/lib/boot2docker/profile
...
export HTTP_PROXY=http://{proxy_host}:{proxy_port}
export HTTPS_PROXY=https://{proxy_host}:{proxy_port}
```

- Restart the docker process
```
sudo /etc/init.d/docker restart
```
(For more details, visit https://nickytd.wordpress.com/2014/07/17/docker-behind-a-proxy/)

## Build Images

### Behind a Proxy

Add in at head of Dockerfile:

>ENV http_proxy http://my_proxy_url.com:<port>

>ENV https_proxy https://my_proxy_url.com:<port>



### Build Basic Python and Tools Image

```
docker build -t cfljam/socker .
```
### Build the Version with R

```
cd PyR
docker build -t cfljam/pyr .
```

## Run Python only version


```
docker run --rm  -v <local dir to mount>:<mount point in VM> -p 8889:8889 -it cfljam/socker
```

- Point your host browser at http://localhost:8889/

## Run Python plus R version

```
docker run -rm -p 8889:8889 -v /my_local_dir:/vm_mount_point -it cfljam/pyr
```

## Note

On OSX or Windows using Boot2docker you will likely  need to open ports in VirtualBox by:

1. Doing this manually

e.g. for port 8889

**Settings->Network -> Port Forwarding**

![PortFwdVB](https://dl.dropboxusercontent.com/u/8064851/images/VirtualBoxPortForwardiPynbExample.png)

2. On OSX consider dvm  http://fnichol.github.io/dvm/
3. Use a modified boot2docker for Vagrant https://github.com/YungSang/boot2docker-vagrant-box
