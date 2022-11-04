# Web Proxy

The compute nodes for the HPRC clusters do not have access to the
internet. In order to allow internet access for compute nodes, you can
enable web proxy when you run interactive or batch jobs on the compute
nodes, by configuration environment variables, *http\_proxy* and
*https\_proxy* or by loading the WebProxy module.

## WebProxy module

For your convenience, a module has been provided to set the appropriate
environment variables automatically.

    module load WebProxy

This is the preferred method whenever it's applicable. Otherwise,
proceed with the manual options below.

## Set up environment variables

To enable web proxy, run these two lines before starting your
interactive programs or add to your job script.

### Terra

    export http_proxy=10.76.5.24:8080
    export https_proxy=10.76.5.24:8080

### Grace

    export http_proxy=10.73.132.63:8080
    export https_proxy=10.73.132.63:8080

## Set up proxy in the browser

You can enable web proxy for Firefox by following
[instruction](https://support.mozilla.org/en-US/kb/connection-settings-firefox)
and provide the IP/port for both HTTP and HTTPS proxies. For Terra, use
10.76.5.24 and port 8080. For Ada, use IP 10.72.2.7 and port 18080. For
Grace, use IP 10.73.132.63 and port 8080.

## Set up proxy in Jupyter Notebook Portal app

Run the following lines in your notebook:

### Terra

    import os
    os.environ['http_proxy'] = '10.76.5.24:8080'
    os.environ['https_proxy'] = '10.76.5.24:8080'

### Grace

    import os
    os.environ['http_proxy'] = '10.73.132.63:8080'
    os.environ['https_proxy'] = '10.73.132.63:8080'
