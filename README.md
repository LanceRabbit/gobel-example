# gobel-example
Gobel is a headless cms built with golang. 

This repository contains the code to run gobel in each environment.

Both local environment and production environment are assumed to be operated with docker-compose.

# gobel
- [gobel-api](https://github.com/bmf-san/gobel-api)
- [gobel-client-example](https://github.com/bmf-san/gobel-client-example)
- [gobel-admin-client-example](https://github.com/bmf-san/gobel-admin-client-example)
- [gobel-example](https://github.com/bmf-san/gobel-example)
- [gobel-ops-example](https://github.com/bmf-san/gobel-ops-example)
- [migrate-rubel-to-gobel](https://github.com/bmf-san/migrate-rubel-to-gobel)

# Get started
## Docker Compose
Work in `./docker-compose` directory.

### Create a network
`make docker-create-network`

### Copy a and edit an .env
If you want to check the operation, just copy .env.example.
Of course, if you want to operate in a production environment, change the settings.

```sh
cp .env.example .env
```

### Edit a /etc/hosts if you run containers on local
There are three host names.

```
ex.
127.0.0.1 SERVER_NAME_OF_API          # use GOBEL_NGINX_API_SERVER_NAME in .env
127.0.0.1 SERVER_NAME_OF_CLIENT       # use GOBEL_NGINX_CLIENT_SERVER_NAME in .env
127.0.0.1 SERVER_NAME_OF_ADMIN_CLIENT # use GOBEL_NGINX_ADMIN_CLIENT_SERVER_NAME .env
```

### Build containers
```sh
make docker-compose-build
```

### Run containers
```sh
make docker-compose-up
```

# Faker
[Here](https://github.com/bmf-san/gobel-api/blob/master/doc/faker.sql) is a fake data sql file that can be used for operation verification.

## Go to applications
|            Application             |                 URL                 |
| ---------------------------------- | ----------------------------------- |
| gobel-api                          | http:/SERVER_NAME_OF_API/           |
| gobel-admin-client-example-example | http://SERVER_NAME_OF_ADMIN_CLIENT/ |
| gobel-client-example               | http://SERVER_NAME_OF_CLIENT/       |
| prometheus                         | http://localhost:9090/graph         |
| node-exporter                      | http://localhost:9100/              |
| mysqld-exporter                    | http://localhost:9104/              |
| grafana                            | http://localhost:3000/              |
| kibana                             | http://0.0.0.0:5601/                |
| redis-insight                      | http://localhost:8001/              |

# Run in production
See [gobel-ops-example](https://github.com/bmf-san/gobel-ops-example) for building infrastructure construction of the production environment.

# Tips
Elasticsearch may not start when changing the version related to fluentd.
In that case, deleting `/elasticsearch/nodes` may solve the problem.

```shell
gobel-grafana is up-to-date
Recreating gobel-elasticsearch ... 
gobel-cadvisor is up-to-date
gobel-node-exporter is up-to-date
Recreating gobel-prometheus    ... 
Recreating gobel-elasticsearch ... done
Recreating gobel-prometheus    ... done
ERROR: for kibana  Container "72a9d83b3ef8" is unhealthy.
ERROR: for fluentd  Container "72a9d83b3ef8" is unhealthy.
Encountered errors while bringing up the project.
make: *** [Makefile:20: docker-compose-up] Error 1
make: *** [deploy] Error 2
```

# UI screenshots
## gobel-client-example
An example application using gobel-api.

<img src="https://user-images.githubusercontent.com/13291041/121388155-33652780-c986-11eb-9076-985b7113b0a9.png" alt="drawing" width="400"/>

## gobel-admin-client-example
An example application using gobel-api for admin.

<img src="https://user-images.githubusercontent.com/13291041/121388150-32cc9100-c986-11eb-86d5-2782bdb6193b.png" alt="drawing" width="400"/>

## Grafana
A dashboard for monitoring various logs in cooperation with prometheus using cAdvisor, mysqld-exporter and node-exporter.

### Container monitoring
Monitor the resource usage and performance characteristics of running containers.

<img src="https://user-images.githubusercontent.com/13291041/121389800-b8047580-c987-11eb-9814-291498c74bd7.png" alt="drawing" width="400"/>

### MySQL Overview
Monitor the MySQL server metrics.

<img src="https://user-images.githubusercontent.com/13291041/121390045-f5690300-c987-11eb-8a1c-d3b4f278e23c.png" alt="drawing" width="400"/>

### Node Exporter Full
Monitor system metrics provided by node exporter.

<img src="https://user-images.githubusercontent.com/13291041/121389862-c8b4eb80-c987-11eb-9be9-2752c13b9218.png" alt="drawing" width="400"/>

## Prometheus
Prometheus is an open-source systems monitoring and alerting toolkit.
Poll the exporter to collect resources and manage data.

<img src="https://user-images.githubusercontent.com/13291041/121389083-0402ea80-c987-11eb-98a5-50908aa36372.png" alt="drawing" width="400"/>

## Node exporter
Node exporter collects system metrics.

<img src="https://user-images.githubusercontent.com/13291041/121389071-006f6380-c987-11eb-85bc-14f0e96b2cbc.png" alt="drawing" width="400"/>

## MySQL exporter
MySQL exporter collects MySQL server metrics.

<img src="https://user-images.githubusercontent.com/13291041/121389074-01a09080-c987-11eb-968e-dc7ae9d3c29c.png" alt="drawing" width="400"/>

## Kibana
Visualization of logs in cooperation with elasticsearch and fluentd.

- Application log
  - gobel-api-*
  - gobel-client-*
- DB log
  - mysql-slow-*
- Web server log
  - nginx-access-*
  - nginx-error-*

The index name above is an example.
See [fluent.conf](https://github.com/bmf-san/gobel-example/blob/master/fluentd/config/fluent.conf) for details.

<img src="https://user-images.githubusercontent.com/13291041/121403338-c22d7080-c995-11eb-82b7-b9470a0f192a.png" alt="drawing" width="400"/>

# License
This project is licensed under the terms of the MIT license.

# Author
bmf - Software engineer.

- [github - bmf-san/bmf-san](https://github.com/bmf-san/bmf-san)
- [twitter - @bmf-san](https://twitter.com/bmf_san)
- [blog - bmf-tech](http://bmf-tech.com/)
