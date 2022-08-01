# Spring PetClinic Sample Application

## Understanding the Spring Petclinic application with a few diagrams

<a href="https://speakerdeck.com/michaelisvy/spring-petclinic-sample-application">See the presentation here</a>

## Deploy Local Container Registry

We will run the containers on its own network,

```shell
docker network create spring-petclinic
```

```shell
docker run -d --network=spring-petclinic \
  -p 5001:5000 \
  --name spring-petclinic-registry \
  registry:2
```

## Trigger the pipeline

```shell
drone exec --env-file=.env --network=spring-petclinic
```

## Running petclinic locally

```shell
docker run -d --rm --name=spring-petclinic \
  -p 8085:8080 \
  --network=spring-petclinic \
  localhost:5001/example/petclinic
```

- From the host we use use `localhost:5001` to access the local registry.
- If you use arm64 machines then try adding the `--platform=linux/arm64` to the docker run command to download the `arm64` image

You can then access petclinic here: <http://localhost:8085/>

<img width="1042" alt="petclinic-screenshot" src="https://cloud.githubusercontent.com/assets/838318/19727082/2aee6d6c-9b8e-11e6-81fe-e889a5ddfded.png">
