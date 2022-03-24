# STAGE 1 (DEV)

FROM  golang:1.18.0-alpine3.15 as dev


# Installing git
# RUN apk update && apk upgrade && apk add --no-cache git
# RUN go get github.com/sirupsen/logrus

WORKDIR /work
COPY ./src /work/


# STAGE 1.5 (BUILD)

FROM golang:1.18.0-alpine3.15 as build
WORKDIR /work
COPY ./src /work/
RUN go build -o app


# STAGE 2 (PROD)

FROM alpine:3.15 as prod
COPY --from=build /work/app /
CMD ./app



