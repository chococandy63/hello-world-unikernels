# hello-world-unikernels
A hello world unikernel image 

# Kraftkit

## Installation

You can quickly and easily install KraftKit using the interactive installer.  Simply run the following command to get started: 

```shell
curl --proto '=https' --tlsv1.2 -sSf https://get.kraftkit.sh | sh
```

Alternatively, you can download the binaries from the [releases pages](https://github.com/unikraft/kraftkit/releases).

### Container build environment

KraftKit ships a container build environment which you can use instead of installing any dependencies directly on your host.
It includes the `kraft` binary as well as all the additional tools and libraries for building Unikraft unikernels.
Simply attach a working directory on your host as a mount path volume mapped to `/workspace`, e.g.:

```shell
docker run -it --rm -v $(pwd):/workspace --entrypoint bash kraftkit.sh/base:latest
```

The above command will drop you into a container shell.
Simply type `exit` or Ctrl+D to quit.

## Quickstart

Building a unikernel with KraftKit is designed to be simple.

Add a `Kraftfile` to your project directory, which specifies the libraries needed for your unikernel:

```yaml
specification: v0.5

unikraft: stable

libraries:
  musl: stable

targets:
  - name: default
    architecture: x86_64
    platform: qemu
```

You can also add an additional `Makefile.uk` which specifies any source files:

```Makefile
$(eval $(call addlib,apphelloworld))

APPHELLOWORLD_SRCS-y += $(APPHELLOWORLD_BASE)/main.c
```

Then it is a case of running:

```shell
cd path/to/workdir

kraft pkg update
kraft build
```

You can run your unikernel using:

```shell
kraft run
```

## License

KraftKit is part of the [Unikraft OSS Project][unikraft-website] and licensed under `BSD-3-Clause`.

[kraftkit-getting-started]: https://unikraft.org/docs/getting-started/
