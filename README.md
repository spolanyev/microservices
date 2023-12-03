# About


The idea came to me when I was given a [test assignment](https://github.com/spolanyev/testJagaad) in PHP to implement an application that retrieves a list of cities from one API and then retrieves weather forecasts for those cities from another API. At the time, I had already implemented a console application in Rust (another [test assignment](https://github.com/spolanyev/testElastio)) that retrieved weather forecasts for a city. I thought it could be used as a microservice in a new application.

I added typical microservice infrastructure such as RabbitMQ for inter-microservice communication and ELK for log analysis and visualization. I then packaged it all in Docker containers.

| Microservice                        | Engine        | Codename      |
|-------------------------------------|---------------|---------------|
| archive-record                      | PostgreSQL    | -             |
| city-provider                       | PHP           | MicroserviceB |
| log-aggregator                      | Logstash      | -             |
| log-storage                         | Elasticsearch | -             |
| log-viewer                          | Kibana        | -             |
| message-broker                      | RabbitMQ      | -             |
| weather-cache                       | Redis         | -             |
| weather-provider                    | Rust          | MicroserviceC |
| website                             | PHP           | MicroserviceA |


A user visits `website`. `website` sends a command to `city-provider`. `city-provider` gets a list of cities and sends it to `weather-provider`. `weather-provider` checks `weather-cache` for fresh results and sends weather forecasts to `website`. `website` stores the data in `archive-record` and displays it to the user.<br> 


The AsyncApi file is [here](asyncapi.yml).


![Running containers](https://github.com/spolanyev/microservices/blob/main/docker-compose-up.png?raw=true)

![Console log](https://github.com/spolanyev/microservices/blob/main/website-rabbitmq-log.png?raw=true)

![Kibana log](https://github.com/spolanyev/microservices/blob/main/kibana-rabbitmq-log.png?raw=true)

# Contacts

If you are hiring, feel free to contact me at [spolanyev@gmail.com](mailto:spolanyev@gmail.com?subject=Microservices)
