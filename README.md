vsFTPd server docker
===================

This docker image extends and distributes the following software:

#### vsFTPd

- Based on [vsftpd project](https://security.appspot.com/vsftpd.html).

# Build the image
The docker image for vsFTPd can be found in the [docker hub](https://hub.docker.com/r/fikipollo/vsftpd/). However, you can rebuild is manually by running **docker build**.

```sh
sudo docker build -t vsftpd .
```
Note that the current working directory must contain the Dockerfile file.

## Running the Container
The recommended way for running your vsFTPd docker is using the provided **docker-compose** script that resolves the dependencies and make easier to customize your instance. Alternatively you can run the docker manually.

## Quickstart

This procedure starts vsFTPd in a standard virtualised environment.

- Install [docker](https://docs.docker.com/engine/installation/) for your system if not previously done.
- `docker run -it -p 21:21 fikipollo/vsftpd`
- vsFTPd will be available at [ftp://localhost:21/](ftp://localhost:21/)

## Using the docker-compose file
Launching your vsFTPd docker is really easy using docker-compose. Just download the *docker-compose.yml* file and customize the content according to your needs. There are few settings that should be change in the file, follow the instructions in the file to configure your container.
To launch the container, type:
```sh
sudo docker-compose up
```
Using the *-d* flag you can launch the containers in background.

In case you do not have the Container stored locally, docker will download it for you.

# Install the image <a name="install" />
You can run manually your containers using the following commands:

```sh
sudo docker run --name vsftpd -v /your/data/location/ftp-data:/home/ -e FTP_USER=myftpuser -e FTP_PASS=supersecret -p 8021:21 -d fikipollo/vsftpd
```

In case you do not have the Container stored locally, docker will download it for you.

A short description of the parameters would be:
- `docker run` will run the container for you.

- `-p 8021:21` will make the port 21 (inside of the container) available on port 8021 on your host.
    Inside the container a vsFTPd server is running on port 21 and that port can be bound to a local port on your host computer.

- `fikipollo/vsftpd` is the Image name, which can be found in the [docker hub](https://hub.docker.com/r/fikipollo/vsftpd/).

- `-d` will start the docker container in daemon mode.

- `-e VARIABLE_NAME=VALUE` changes the default value for a system variable.
The vsFTPd docker accepts the following variables that modify the behavior of the system in the docker. All variables are optional.

    - **FTP_USER**, the name for the default ftp account. Default is _ftpuser_.
    - **FTP_PASS**, the password for the default ftp account. Default is _supersecret_.
    - **FTP_HOME**, the home directory for the default ftp account. Default value: _/home/$FTP_USER_.
    - **FTP_UID**, the user and group id for the default ftp account. Default value: _1000_.
    - **ONLY_UPLOAD**, set to _YES_ to disable data download. By default download is enabled (i.e. default value is _NO_).
    - **PASV_ENABLE**, set to _YES_ to enable passive mode (PASV). By default PASV mode is disabled (i.e. default value is _NO_).
    - **PASV_ADDRESS**, if PASV mode is enabled, you may need to specify the IP address (external) or the URL to your FTP server. Default value: _127.0.0.1_.
    - **PASV_MIN**, the minimum port number used for PASV mode. Default value: _21200_.
    - **PASV_MAX**, the maximum port number used for PASV mode. Default value: _21210_.

Note that if you enable PASV mode, the internal ports used for passive mode (i.e. ports PASV_MIN to PASV_MAX) should be mapped to external ports (same ports). For example, if PASV_MIN=21100 and PASV_MAX=21110, you should add the option _-p 21100-21110_.

# Version log
  - v0.9 October 2017: First version of the docker.
