FROM golang:alpine as builder

RUN apk update && apk add --no-cache git

WORKDIR /app

COPY . .

RUN go mod tidy

RUN go build -o bin

FROM alpine:latest

WORKDIR /app

COPY --from=builder /app/bin .

COPY --from=builder /app/dev-docker.env .

ENV APP_ENV=dev-docker

ENTRYPOINT [ "/app/bin" ]
