FROM golang:alpine

WORKDIR /app

COPY pokedex-cli /app

RUN go build -o pokedexcli

ENTRYPOINT ["./pokedexcli"]