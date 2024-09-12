# try-devcontainer
This is a simple project to show case how to use Meta (a tool for managing multi-project systems and libraries) and Dev Containers along with Docker to manage your local development environment.

## Description
Consider an application built on a microservice architecture, utilizing Confluent for streaming and MongoDB for storage, with the source code for each microservice distributed across several GitHub repositories.

Traditionally, developers would be asked to clone multiple repositories, install compilers, interpreters, and necessary tools locally, and use Docker Compose to start the required Docker containers.

Let's see how we can streamline the process!

## Getting Started

### Dependencies

Make sure you have the following dependencies installed on your local machine.

* [Visual Code Studio](https://code.visualstudio.com/download) and [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension 
* [Docker](https://docs.docker.com/desktop/install/mac-install/)
* [docker-compose](https://formulae.brew.sh/formula/docker-compose)
* [Node (via nvm)](https://github.com/nvm-sh/nvm) (for running Meta; the latest LTS is fine or other versions supported by Meta)
* [Meta](https://github.com/mateodelnorte/meta)

### Running the Sample

* Clone the repository, 
```bash
╰─ git clone git@github.com:eraserx99/try-devcontainer.git
Cloning into 'try-devcontainer'...
remote: Enumerating objects: 74, done.
remote: Counting objects: 100% (74/74), done.
remote: Compressing objects: 100% (42/42), done.
remote: Total 74 (delta 30), reused 64 (delta 20), pack-reused 0 (from 0)
Receiving objects: 100% (74/74), 11.90 KiB | 1.70 MiB/s, done.
Resolving deltas: 100% (30/30), done.
```
* Pull down the source code from other microservice repositories (they're definied in the .meta file)
```bash
╰─ cd try-devcontainer
╰─ meta git update

*** the following repositories have been added to .meta but are not currently cloned locally:
*** {
  'try-go': 'git@github.com:eraserx99/try-go.git',
  'try-node': 'git@github.com:eraserx99/try-node.git',
  'try-java': 'git@github.com:eraserx99/try-java.git',
  'try-java-kafka': 'git@github.com:eraserx99/try-java-kafka.git'
}
*** type 'meta git update' to correct.

/Users/steve/workspace.go/try-devcontainer/try-java-kafka:
Cloning into 'try-java-kafka'...
remote: Enumerating objects: 208, done.
remote: Counting objects: 100% (208/208), done.
remote: Compressing objects: 100% (126/126), done.
remote: Total 208 (delta 54), reused 185 (delta 32), pack-reused 0 (from 0)
Receiving objects: 100% (208/208), 79.27 KiB | 1.12 MiB/s, done.
Resolving deltas: 100% (54/54), done.
/Users/steve/workspace.go/try-devcontainer/try-java-kafka ✓

/Users/steve/workspace.go/try-devcontainer/try-java:
Cloning into 'try-java'...
remote: Enumerating objects: 74, done.
remote: Counting objects: 100% (74/74), done.
remote: Compressing objects: 100% (45/45), done.
remote: Total 74 (delta 6), reused 73 (delta 5), pack-reused 0 (from 0)
Receiving objects: 100% (74/74), 57.89 KiB | 1.38 MiB/s, done.
Resolving deltas: 100% (6/6), done.
/Users/steve/workspace.go/try-devcontainer/try-java ✓

/Users/steve/workspace.go/try-devcontainer/try-node:
Cloning into 'try-node'...
remote: Enumerating objects: 16, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 16 (delta 0), reused 16 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (16/16), 17.05 KiB | 2.13 MiB/s, done.
/Users/steve/workspace.go/try-devcontainer/try-node ✓

/Users/steve/workspace.go/try-devcontainer/try-go:
Cloning into 'try-go'...
remote: Enumerating objects: 16, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 16 (delta 0), reused 16 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (16/16), 9.61 KiB | 819.00 KiB/s, done.
/Users/steve/workspace.go/try-devcontainer/try-go ✓
```
* Run Visual Code Studio and open this try-devcontainer folder. Give Visual Code Studio a couple of seconds and it will ask you if you wanna **Reopen in Container**. Click it and it will show you four pre-defined Dev Containers in this project
  * try-go
  * try-java
  * try-java-kafka
  * try-java-node
* Pick any one of them, and Visual Code Studio will instruct Docker to download and run some images, including your Dev Containers, specified in the docker-compose file and a couple of devcontainer.json files under .devcontainer directory. Once the download is complete, you'll be able to start working on your project directly within the container.
* You can also run some Docker command to check the other contianers.
```
╰─ docker ps -a
CONTAINER ID   IMAGE                                                                                   COMMAND                  CREATED         STATUS         PORTS                                            NAMES
75987d06bbed   confluentinc/cp-ksqldb-cli:7.7.0                                                        "/bin/sh"                2 minutes ago   Up 2 minutes                                                    ksqldb-cli
1aa811a5b1fb   confluentinc/cp-enterprise-control-center:7.7.0                                         "/etc/confluent/dock…"   2 minutes ago   Up 2 minutes   0.0.0.0:9021->9021/tcp                           control-center
0d8e832f4a77   confluentinc/ksqldb-examples:7.7.0                                                      "bash -c 'echo Waiti…"   2 minutes ago   Up 2 minutes                                                    ksql-datagen
e4b23f6f2e4e   confluentinc/cp-ksqldb-server:7.7.0                                                     "/etc/confluent/dock…"   2 minutes ago   Up 2 minutes   0.0.0.0:8088->8088/tcp                           ksqldb-server
cd7942f46043   cnfldemos/cp-server-connect-datagen:0.6.4-7.6.0                                         "/etc/confluent/dock…"   2 minutes ago   Up 2 minutes   0.0.0.0:8083->8083/tcp, 9092/tcp                 connect
21303b46a3a3   obsidiandynamics/kafdrop                                                                "/kafdrop.sh"            2 minutes ago   Up 2 minutes   0.0.0.0:9000->9000/tcp                           kafdrop
115a3782a57d   confluentinc/cp-kafka-rest:7.7.0                                                        "/etc/confluent/dock…"   2 minutes ago   Up 2 minutes   0.0.0.0:8082->8082/tcp                           rest-proxy
620faadd2853   confluentinc/cp-schema-registry:7.7.0                                                   "/etc/confluent/dock…"   2 minutes ago   Up 2 minutes   0.0.0.0:8081->8081/tcp                           schema-registry
df2004fe13b3   mongo                                                                                   "docker-entrypoint.s…"   2 minutes ago   Up 2 minutes   27017/tcp                                        mongo
a2c0a05a48e3   confluentinc/cp-kafka:7.7.0                                                             "/etc/confluent/dock…"   2 minutes ago   Up 2 minutes   0.0.0.0:9092->9092/tcp, 0.0.0.0:9101->9101/tcp   broker
68b004514c9a   vsc-try-devcontainer-48126117ad1b9206bb5e8d18b0af8f9821e5878b2051828806d51394451b9b79   "/bin/sh -c 'echo Co…"   2 minutes ago   Up 2 minutes                                                    try-java-kafka
117667b2798f   mcr.microsoft.com/devcontainers/javascript-node:20-bookworm                             "docker-entrypoint.s…"   2 minutes ago   Up 2 minutes                                                    try-node
c21c24cad670   mcr.microsoft.com/devcontainers/go:1-1.23-bookworm                                      "/bin/sh -c 'while s…"   2 minutes ago   Up 2 minutes                                                    try-go
a5e54eba5fe3   mcr.microsoft.com/devcontainers/java:21-jdk-bookworm                                    "/bin/sh -c 'while s…"   2 minutes ago   Up 2 minutes                                                    try-java
efe07ebc7686   mongo-express                                                                           "/sbin/tini -- /dock…"   2 minutes ago   Up 2 minutes   0.0.0.0:8888->8081/tcp                           mongo-express
```
* This demo doesn't stop the containers when you disconnect from your Dev Containers. You can run docker-compose command to bring everything down manually.
```
╰─ docker-compose down
```

Overall, this is just a sample project to demostrate how to use Meta and Dev Containers to simplify the developer setup. It can support other usage cases such as remote development and debugging accordingly too. You might want to check other reference documents below.
 
 * https://code.visualstudio.com/docs/devcontainers/containers
 * https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/introduction-to-dev-containers
 * https://www.daytona.io/dotfiles/ultimate-guide-to-dev-containers
 * https://code.visualstudio.com/remote/advancedcontainers/develop-remote-host


