build: minecraft.tar.bz2
	docker-compose build minecraft

minecraft.tar.bz2: $(wildcard bedrock-server-*.zip)
	unzip -d minecraft bedrock-server-*.zip
	tar cvjf minecraft.tar.bz2 minecraft
	rm -rf minecraft

push: build
	docker-compose push minecraft

deploy: push
	docker context use {{cookiecutter.docker_context}}
	docker stack deploy -c docker-compose.yml minecraft
	docker context use default
