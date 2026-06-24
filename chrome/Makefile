.PHONY: get-version build test tags

CURRENT_DIR:=$(shell dirname $(realpath $(firstword $(MAKEFILE_LIST))))

get-version:
	@docker pull --quiet chromedp/headless-shell:stable > /dev/null 2>&1
	@docker inspect chromedp/headless-shell:stable --format '{{index .Config.Labels "org.opencontainers.image.version"}}' 2>/dev/null || echo "stable"

build:
	@docker buildx build --platform linux/amd64,linux/arm64 \
		--tag brightsec/nextools-chrome \
		--tag 454884832027.dkr.ecr.us-east-1.amazonaws.com/nextools-chrome \
		--push $(CURRENT_DIR)

build-local:
	@docker build --tag brightsec/nextools-chrome $(CURRENT_DIR)

test:
	@docker run --detach --publish 9222:9222 --name nextools-chrome brightsec/nextools-chrome
	@timeout 20s sh -c "trap 'docker container rm --force nextools-chrome' 0; until curl http://localhost:9222/json/version; do sleep 1; done"
