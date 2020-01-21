FROM golang AS builder
WORKDIR /go/src/app
RUN go get github.com/nats-io/nats.go
RUN git clone https://github.com/nats-io/nats.go.git
RUN cd /go/src/app/nats.go/examples/nats-pub/; CGO_ENABLED=0 CGO=linux go build -o pub
RUN cd /go/src/app/nats.go/examples/nats-sub/; CGO_ENABLED=0 CGO=linux go build -o sub

FROM alpine
RUN apk add --no-cache bash
COPY --from=builder /go/src/app/nats.go/examples/nats-sub/sub /bin/sub
COPY --from=builder /go/src/app/nats.go/examples/nats-pub/pub /bin/pub

CMD ["/bin/sh"]