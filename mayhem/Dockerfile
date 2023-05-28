# Build Stage:
FROM --platform=linux/amd64 ubuntu:20.04 as builder

## Install build dependencies.
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y gcc make cmake build-essential

## Add Source Code
ADD / /wje-mayhem
WORKDIR /wje-mayhem

## Build Step
RUN rm -rf build && mkdir build \
   && cd build
   # && cmake .. \
   # && make

# Package Stage
FROM --platform=linux/amd64 ubuntu:20.04
COPY --from=builder /wje-mayhem /
# COPY --from=builder /wje-mayhem/build/src/cli/wjecli /


# COPY --from=builder /wje-mayhem /