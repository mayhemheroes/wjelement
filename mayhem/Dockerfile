# Build Stage:
FROM --platform=linux/amd64 ubuntu:20.04 as builder

## Install build dependencies.
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y clang make cmake build-essential

## Add Source Code
ADD / /wje-mayhem
WORKDIR /wje-mayhem


## Build Step 
RUN rm -rf build && mkdir build \
   && cd build \
   && cmake .. \
   && make
   

# Package Stage
FROM --platform=linux/amd64 ubuntu:20.04
COPY --from=builder /wje-mayhem/build/src/cli/wjecli /
COPY --from=builder /wje-mayhem/build/src /lib
# COPY --from=builder /wje-mayhem/build/src/cli/wjecli /
# COPY --from=builder /wje-mayhem /

# Instructions to get the built libraries into a common place to have the executable load them
RUN cd ~ \
   && cp -a /lib/wjelement/. /lib/ \
   && cp -a /lib/wjwriter/. /lib/ \
   && cp -a /lib/wjreader/. /lib/ \
   && cp -a /lib/lib/. /lib/