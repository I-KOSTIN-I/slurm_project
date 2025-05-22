
FROM golang:1.24-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN go build -o backend .


FROM alpine:3.21.3

WORKDIR /app

COPY --from=builder /app/backend .

EXPOSE 8080

HEALTHCHECK --interval=10s --timeout=2s --start-period=5s CMD wget -q --spider http://localhost:8080/healthz || exit 1

CMD ["./backend"]
