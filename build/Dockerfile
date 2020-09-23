# stage 1 building the code
FROM golang:1.15 as builder

# don't place it into $GOPATH/bin because Drone mounts $GOPATH as volume
RUN --mount=target=/build https://github.com/golangci/golangci-lint
#RUN git clone https://github.com/golangci/golangci-lint
WORKDIR golangci-lint
RUN go build -o /dist/golangci-lint ./cmd/golangci-lint/main.go

# stage 2
FROM golang:1.15
# don't place it into $GOPATH/bin because Drone mounts $GOPATH as volume
COPY --from=builder /dist/golangci-lint /usr/bin/
CMD ["golangci-lint"]
