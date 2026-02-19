FROM golang:alpine

WORKDIR /app

COPY pokedex-cli/go.mod ./
RUN go mod download

COPY pokedex-cli/ .

RUN go build -o pokedexcli

CMD ["sleep", "infinity"]