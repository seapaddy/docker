ifndef VERBOSE
.SILENT:
endif

build-python-poetry:
	docker build \
		--build-arg USER=$(shell whoami) \
		--build-arg UID=$(shell id -u) \
		--build-arg GID=$(shell id -g) \
		-t poetry:0.1 .
