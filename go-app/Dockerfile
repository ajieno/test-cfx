# Build stage
FROM golang:1.21 AS builder

WORKDIR /app
COPY . .

RUN go build -o app

# Final stage
FROM gcr.io/distroless/base

COPY --from=builder /app/app /app

EXPOSE 8080
ENTRYPOINT ["/app"]
