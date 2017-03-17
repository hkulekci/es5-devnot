## Prepare Your Environment

First of all, we need [Docker](https://www.docker.com/) to be able to build
the environment. Please donwload and install te docker. Check 
[the documentation](https://docs.docker.com/learn/) for more information about 
installation.

After installing, we check out files. We have a `.docker` folder to configure 
docker containers. Each folder in the `.docker` folder represent our services. 
For example, we have Elasticsearch configuration files and installation scripts
in the `elasticsearch` folder, etc.

```
.docker
├── beat
│   ├── Dockerfile
│   └── filebeat.yml
├── elasticsearch
│   ├── Dockerfile
│   └── config
│       ├── elasticsearch.yml
│       └── logging.yml
├── kibana
│   └── Dockerfile
└── logstash
    ├── Dockerfile
    └── conf
        ├── logstash.conf
        └── template.json
```

You can carry on the study about docker and environment but we will talk about 
Elasticsearch and Elastic products. Following command will help you about easy 
starting.

```
docker-compose build
docker-compose up elasticsearch kibana logstash
```

With these scripts, we start our elasticsearch, kibana and logstash services.