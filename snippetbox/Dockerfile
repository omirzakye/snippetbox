FROM golang

COPY . /goyer

WORKDIR /goyer

RUN go mod download

ENV GO111MODULE=on\
    CGO_ENABLED=0\
    GOOS=linux\
    GOARCH=amd64
RUN go build /goyer/cmd/web && chmod +x /goyer/cmd/web

ENTRYPOINT ["./web"]

FROM alpine:latest

RUN apk --no-cache add ca-certificates

WORKDIR /root/

COPY --from=0 /goyer .

CMD ["./web"]

EXPOSE 4000