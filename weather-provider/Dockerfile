FROM rust:1.66.1

RUN apt-get update && apt-get install -y git netcat

RUN git clone https://github.com/spolanyev/testElastio.git

WORKDIR /testElastio

RUN git checkout 5303198cb3c05984725f98e23d8410b7b3e3a960

COPY preferences /root/.config/testelastio/preferences

RUN cargo build --release

COPY .env /.env

COPY app /app

WORKDIR /app

RUN cargo update && cargo build --release

CMD until nc -z message-broker 5672; do echo Waiting for RabbitMQ; sleep 1; done; /app/target/release/app
