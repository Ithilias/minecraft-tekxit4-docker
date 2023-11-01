# minecraft-tekxit4-docker

Dockerfiles to run a Minecraft [tekxit4](https://www.technicpack.net/modpack/tekxit-4-official.1921233) server.

## Usage

### Setting up the server

```sh
git clone https://github.com/Ithilias/minecraft-tekxit4-docker.git
cd minecraft-tekxit4-docker

# server data will be written to ./data by default. You might want to change the volume before you continue.
# memory limits can be set by changing the environment variables in the compose file.

# Set the EULA environment variable to true to automatically accept the Minecraft EULA.
# Set the RCON_PORT and RCON_PASSWORD environment variables to configure the RCON port and password.

docker compose up
```

Alternatively, you can use the Docker image available as a package on GitHub.
Here's an example `docker-compose.yml` file for using the Docker image:

```yaml
version: '3.9'

services:
  tekxit:
    container_name: tekxit
    image: ghcr.io/ithilias/minecraft-tekxit4-docker:latest
    environment:
      JAVA_XMS: "4G"
      JAVA_XMX: "12G"
      EULA: "true"
      RCON_PORT: "25575"
      RCON_PASSWORD: "foobar"
    volumes:
      - ./data:/data
    ports:
      - "25565:25565"
```

The server will now be installed to the data volume.

### Accessing the console

This image comes with [rcon-cli](https://github.com/itzg/rcon-cli) preinstalled. The RCON port and password can be configured using the `RCON_PORT` and `RCON_PASSWORD` environment variables in the docker-compose file.

To access the console, you can use the `mc-command.sh` script:

```sh
./mc-command.sh -h
```
