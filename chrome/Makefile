.PHONY: get-version build build-local test

CURRENT_DIR:=$(shell dirname $(realpath $(firstword $(MAKEFILE_LIST))))
IMAGE_NAME:=brightsec/nextools-chrome
ECR_IMAGE:=454884832027.dkr.ecr.us-east-1.amazonaws.com/nextools-chrome

get-version:
	@docker run --rm debian:bookworm-slim sh -c \
		"apt-get update -qq 2>/dev/null && apt-cache show chromium 2>/dev/null | sed -n 's/^Version: \([0-9.]*\).*/\1/p' | head -1"

build:
	@docker build --tag $(IMAGE_NAME) --tag $(ECR_IMAGE) $(CURRENT_DIR)

build-local:
	@docker build --tag $(IMAGE_NAME) $(CURRENT_DIR)

test:
	@docker run --detach --publish 9222:9222 --name nextools-chrome $(IMAGE_NAME)
	@timeout 20s sh -c "trap 'docker container rm --force nextools-chrome' 0; until curl -s http://localhost:9222/json/version; do sleep 1; done"
