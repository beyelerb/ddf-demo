# DIB Docker Image

## Usage

### Simple

Simple usage: run `docker container run -it -p 8993:8993 docker-dib.di2e.net/dib/dib:<version>` 

### Advanced

The dib docker image supports automatic configuration and installation of many features through the use of environment variables.
These can be passed into the container at runtime to bootstrap a usable system.

For a full list of options see the [documentation](https://github.com/oconnormi/docker-ddf-base/blob/master/README.md#features)
