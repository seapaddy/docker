ifndef VERBOSE
.SILENT:
endif

build-development-docker:
	docker build \
		--build-arg USER=$(shell whoami) \
		--build-arg UID=$(shell id -u) \
		--build-arg GID=$(shell id -g) \
		-t developer:latest .

run-devel:
	docker run \
		-it --rm \
		--net=host \
		-e TERM=st-256color \
		-v ${PWD}:${HOME}/app \
		-v ${HOME}/.config/nvim/:${HOME}/.config/nvim \
		-v ${HOME}/.config/tmux/:${HOME}/.config/tmux/ \
		-v ${HOME}/.config/zsh/:${HOME}/.config/zsh/ \
		-v ${HOME}/.local/share/nvim/:${HOME}/.local/share/nvim \
		-v ${HOME}/.local/share/zsh/:${HOME}/.local/share/zsh \
		developer /bin/zsh

