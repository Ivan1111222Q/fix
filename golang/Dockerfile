FROM golang:1.22 AS builder
WORKDIR /src
RUN apt-get update && apt-get install -y --no-install-recommends \
        krb5-user curl wget \
        && rm -rf /var/lib/apt/lists/*
COPY . .
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -ldflags="-s -w" -o app main.go
    
FROM scratch
COPY --from=builder /src/app /app
CMD ["/app"]

#Добавил два этапа – builder (сборка) и финальный FROM scratch.
#Добавил все RUN команды в один слой
#Добавил RUN с apt-get update, установкой нужных пакетов (krb5-user curl wget) 
#Очистка кэша (rm -rf /var/lib/apt/lists/*), плюс флаг --no-install-recommends(не тащит лишние зависимости). 