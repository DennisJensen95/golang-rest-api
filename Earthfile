VERSION 0.6
FROM golang:latest
WORKDIR /rest-api

source-files:
    COPY go.mod go.mod
    COPY go.sum go.sum
    COPY config config
    COPY internal internal
    COPY cmd cmd

build:
    FROM +source-files
    RUN go build -o bin/app ./cmd/app
    SAVE ARTIFACT ./bin/app AS LOCAL ./bin/app

run-unit-test:
    FROM +source-files
    RUN go test ./...

