all: build

build:
	docker build --tag cloudgenius/fedora:24-demo .

push: build
	docker push cloudgenius/fedora:24-demo
