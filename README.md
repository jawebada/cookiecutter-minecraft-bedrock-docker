# Docker swarm stack for the bedrock Minecraft server

## Summary

This is a [Cookiecutter](https://cookiecutter.readthedocs.io) template to
configure a docker stack called `minecraft` for the [Minecraft bedrock
server](https://www.minecraft.net/en-us/download/server/bedrock/), which can be
easily deployed to a docker swarm node.

Players are whitelisted and you will be asked for the operator's Minecraft name
and XUID.

The world will be saved in a volume created by the docker-compose file. 

*If your docker swarm consists of multiple nodes, you will have to add label
constraints to [control the placement of the
container](https://success.docker.com/article/using-contraints-and-labels-to-control-the-placement-of-containers).*
PRs are welcome.

## How to use

### Set up the docker swarm

* [Install docker](https://docs.docker.com/get-docker/)
* `docker swarm init`
* Create a corresponding [docker context](https://docs.docker.com/engine/context/working-with-contexts/#create-a-new-context) on your dev machine
* [Set up a (temporary) registry](https://docs.docker.com/registry/deploying/#run-a-local-registry) or sign up to [Docker Hub](https://hub.docker.com)

### Build and deploy the stack on your dev machine

* Install `docker` and `docker-compose`
* Install [Cookiecutter](https://cookiecutter.readthedocs.io/)
  - `apt-get install cookiecutter` or
  - `python3 -m venv env && . env/bin/activate && pip install cookiecutter`
* `cookiecutter gh:jawebada/cookiecutter-minecraft-bedrock-docker`
* Configure your bedrock server stack
  - project_slug: the name of the directory your configuration will be saved to
  - server_name: the name of your Minecraft server
  - level_name: the name of the Minecraft level your server will create
  - game_mode: the default game mode of your server ("survival", "creative", or "adventure"), can be changed by the operator
  - difficulty: the difficulty of your world ("peaceful", "easy", "normal", or "hard")
  - operator_name: the Minecraft name of your server's operator
  - operator_xuid: the XUID of your server's operator
  - published_udp_port: the UDP port that will be published on your docker swarm node
  - docker_context: the name of the docker context for your docker swarm node
  - registry_prefix: this is either your Docker Hub user name or *hostname:port* for your private registry
* `cd your-configuration-directory`
* Download the [latest bedrock server software for ubuntu](https://www.minecraft.net/en-us/download/server/bedrock/) and save it in your configuration directory
* Optionally, edit `whitelist.json`, `server.properties`, or `permissions.json` as required
* `make && make deploy`
* Add the fully qualified domain name and the port of your new server to the server tab of your Minecraft client
* Have fun!

### Update the server

If a new release of the bedrock server becomes available, which does not
introduce breaking changes, you can simply replace the zip file in your build
directory an call `make && make deploy` again.
