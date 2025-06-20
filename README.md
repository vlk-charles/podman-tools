# podman-tools
These tools help with things that I was missing a simple command for from
the upstream project. They were written for and tested with Podman but might
also work with Docker with some modifications.

## Prerequisites
The tools are of no use without Podman itself. The tools call the `podman`
bianry. Other prerequisites are `tar` (tested with GNU), `jq`, and standard Unix
tools.

## Installation
The tools are simple scripts that should be interpretable by any POSIX shell.
To install them, simply copy the contents of `bin` to `/usr/local/bin`,
`~/.local/bin`, or a similar location.

## `podman-expose`
Creates a proxy container to expose a port of an alreeaedy created and possibly
running container. The container can be stopped and rmoved with a simple
`podman stop`.

### Arguments
1. Podman netowrk name
2. Podman container name lookable up in above network's DNS
3. Podman container port
4. Host port, optionally preceded by IP address and `:`

## `podman-expose`
Calls `podman-expose` and then attaches to the proxy container. Arguments have
the same meaning.

## `podman-save-delta`
Uses `podman save` to save an image to an archive and strips the given number
of lower layers. Useful for distributing small changes to an otherwise large
image if a proper registry is not available. The resulting archive most probably
violates the format standard but if the missing lower layers are already present
in the storage of the importing instance, no error is raised.

### Arguments
1. image name prefix; Will not be used for output file name.
2. main part of image name, possibly including tag; Will also be used to form
   output file name.
3. number of base layers to remove
