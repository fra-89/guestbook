# Stage 1: Build stage
FROM golang:1.18 AS builder

WORKDIR /app

# Copia il file main.go
COPY main.go .

# Configura i moduli Go e costruisci l'eseguibile
RUN go mod init guestbook
RUN go mod tidy

RUN go build -o main main.go

# Stage 2: Production stage
FROM ubuntu:18.04

# Copia il binario dal builder
COPY --from=builder /app/main /app/guestbook

# Aggiungi i file pubblici
ADD public/index.html /app/public/index.html
ADD public/script.js /app/public/script.js
ADD public/style.css /app/public/style.css
ADD public/jquery.min.js /app/public/jquery.min.js

# Imposta la directory di lavoro
WORKDIR /app

# Esponi la porta 3000 per l'applicazione
EXPOSE 3000

# Definisci il comando di default per avviare l'app
CMD ["./guestbook"]

