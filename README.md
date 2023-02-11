# About


The idea came to me when I received a [test task](https://github.com/spolanyev/testJagaad) in PHP to implement an application that retrieves a list of cities from one API and then obtains weather forecasts for those cities from another API. At the time, I had already implemented a command-line program in Rust (it was another [test task](https://github.com/spolanyev/testElastio)), which obtains weather forecasts for a city. I thought that it may be used as a microservice in a new application.

I added typical microservice infrastructure, such as RabbitMQ for communication between microservices and ELK for log analyzing and visualizing. I then packaged it all in Docker containers.

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


A user visits the Website. The Website sends a command to the City Provider. The City Provider obtains a list of cities and sends it to the Weather Provider. The Weather Provider checking fresh results in the Weather Cache sends weather forecasts to the Website. The Website stores the data in the Archive Record and displays it to the user.<br> 


The AsyncApi file is [here](asyncapi.yml).


![Running containers](https://github.com/spolanyev/microservices/blob/main/docker-compose-up.png?raw=true)

![Console log](https://github.com/spolanyev/microservices/blob/main/website-rabbitmq-log.png?raw=true)

![Kibana log](https://github.com/spolanyev/microservices/blob/main/kibana-rabbitmq-log.png?raw=true)

# Contacts

If you are hiring, contact me at [spolanyev@gmail.com](mailto:spolanyev@gmail.com?subject=Vacancy)
