FROM golang:1.22-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . ./

RUN go build -o /bin/app ./cmd/api-server


# Start of the resulting final image
# No credentials should be used beyond this point!
FROM gcr.io/distroless/base-debian11

COPY --from=builder /bin/app /bin/app

EXPOSE 8088

CMD ["/bin/app"]
