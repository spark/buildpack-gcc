# Buildpack for GCC
Buildpack for modern (HAL based) Particle firmware against regular gcc.

[![Build Status](https://travis-ci.org/spark/buildpack-gcc.svg)](https://travis-ci.org/spark/buildpack-gcc) [![](https://imagelayers.io/badge/particle/buildpack-gcc:latest.svg)](https://imagelayers.io/?images=particle/buildpack-gcc:latest 'Get your own badge on imagelayers.io')

| |
|---|
| **GCC (you are here)** |
| [Base](https://github.com/spark/buildpack-base) |

This image inherits [base buildpack](https://github.com/spark/buildpack-base).

## Building image

**Before building this image, build or pull [buildpack-base](https://github.com/spark/buildpack-base).**

```bash
$ export BUILDPACK_IMAGE=gcc
$ git clone "git@github.com:spark/buildpack-${BUILDPACK_IMAGE}.git"
$ cd buildpack-$BUILDPACK_IMAGE
$ ./scripts/build-and-push
```

## Running

```bash
$ mkdir -p ~/tmp/input && mkdir -p ~/tmp/output && mkdir -p ~/tmp/cache
$ docker run --rm \
  -v ~/tmp/input:/input \
  -v ~/tmp/output:/output \
  -v ~/tmp/cache:/cache \
  -e FIRMWARE_REPO=https://github.com/spark/firmware.git#v0.5.3-rc.2 \
  -e PLATFORM_ID=3 \
  particle/buildpack-gcc
```

### Input files
Source files have to be placed in `~/tmp/input`

### Output files
After build `~/tmp/output` will be propagated with:

* `run.log` - `stdout` combined with `stderr`
* `stderr.log` - contents of `stderr`, usefull to parse `gcc` errors

**Files only available if compilation succeeds:**
* `firmware.bin` - compiled firmware
* `memory-use.log` - firmware memory use
