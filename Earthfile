VERSION 0.6
FROM golang:1.18
WORKDIR /rest-api

source-files:
    COPY go.mod go.mod
    COPY go.sum go.sum
    COPY config config
    COPY internal internal
    COPY cmd cmd

build:
    FROM +source-files
    RUN go build -o bin/app -ldflags '-linkmode external -w -extldflags "-static"' ./cmd/app
    SAVE ARTIFACT config/config.yml
    SAVE ARTIFACT bin/app
    SAVE ARTIFACT bin/app AS LOCAL bin/app

run-unit-test:
    FROM +source-files
    RUN go test ./...

application-image:
    FROM golang:1.18-alpine
    WORKDIR /application
    COPY +build/config.yml ./config/config.yml
    COPY +build/app ./
    ENTRYPOINT ["./app"]
    SAVE IMAGE go-rest-api:latest

