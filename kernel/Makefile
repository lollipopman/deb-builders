ARTIFACTS?=$(shell pwd)/artifacts
CONFIGS?=$(shell pwd)/configs
CONFIG=config-5.10.0-8-amd64-debian-upstream
CODENAMES?=bullseye
VERSION?=5.10.46
EXTRA_VERSION?=1
ORG?=wmf
TARBALL?=https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-${VERSION}.tar.xz

.PHONY: build_container
build_container:
	mkdir -p $(ARTIFACTS)
	$(foreach CODENAME,$(CODENAMES), \
		buildah build \
			--build-arg CODENAME=$(CODENAME) \
			-t kernel_$(CODENAME) ; \
	)

.PHONY: build_kernel
build_kernel:
	mkdir -p $(ARTIFACTS)
	$(foreach CODENAME,$(CODENAMES), \
		podman run --rm \
			-v $(ARTIFACTS):/artifacts \
			-v $(CONFIGS):/configs \
			-e VERSION=$(VERSION) \
			-e CONFIG=$(CONFIG) \
			-e EXTRA_VERSION=$(EXTRA_VERSION) \
			-e ORG=$(ORG) \
			-e TARBALL=$(TARBALL) \
			localhost/kernel_$(CODENAME):latest ; \
	)
	tree $(ARTIFACTS)
