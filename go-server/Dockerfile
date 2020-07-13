FROM golang:1.12.7-alpine3.10 AS builder
RUN apk add git

RUN mkdir -p /go/src/github.com/moznobkin/product-aggregation-composite
COPY . /go/src/github.com/moznobkin/product-aggregation-composite
WORKDIR /go/src/github.com/moznobkin/product-aggregation-composite

ENV GO111MODULE=on
RUN go build -v -o /go/bin/product-aggregation-composite.exe

FROM alpine:3.10
LABEL maintainer="Michael Oznobkin <oznobkin@gmail.com>"

COPY --from=builder /go/bin/product-aggregation-composite.exe /usr/bin/product-aggregation-composite.exe
COPY --from=builder /go/src/github.com/moznobkin/product-aggregation-composite/data/json/  /usr/data/json/

WORKDIR /usr/bin

EXPOSE 8081 8081
ENTRYPOINT ["/usr/bin/product-aggregation-composite.exe"]
