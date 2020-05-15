build:
	docker-compose build minecraft

push: build
	docker-compose push minecraft

deploy: push
	docker context use {{cookiecutter.docker_context}}
	docker stack deploy -c docker-compose.yml minecraft
	docker context use default
