############################
# STEP 1 build executable binary
############################
FROM alpine AS builder

# Install git and build dependencies.
RUN apk update && apk add --no-cache git make gcc build-base

ENV VERSION=v1.12

RUN git clone --depth 1 --branch "${VERSION}" https://github.com/beanstalkd/beanstalkd.git

WORKDIR /beanstalkd

RUN make

############################
# STEP 2 build a image
############################
FROM alpine

# Import from the builder.
COPY --from=builder /beanstalkd/beanstalkd /usr/bin/beanstalkd

EXPOSE 11300
ENTRYPOINT ["/usr/bin/beanstalkd"]