<a href="https://elest.io">
  <img src="https://elest.io/images/elestio.svg" alt="elest.io" width="150" height="75">
</a>

[![Discord](https://img.shields.io/static/v1.svg?logo=discord&color=f78A38&labelColor=083468&logoColor=ffffff&style=for-the-badge&label=Discord&message=community)](https://discord.gg/4T4JGaMYrD "Get instant assistance and engage in live discussions with both the community and team through our chat feature.")
[![Elestio examples](https://img.shields.io/static/v1.svg?logo=github&color=f78A38&labelColor=083468&logoColor=ffffff&style=for-the-badge&label=github&message=open%20source)](https://github.com/elestio-examples "Access the source code for all our repositories by viewing them.")
[![Blog](https://img.shields.io/static/v1.svg?color=f78A38&labelColor=083468&logoColor=ffffff&style=for-the-badge&label=elest.io&message=Blog)](https://blog.elest.io "Latest news about elestio, open source software, and DevOps techniques.")

# Gitness, verified and packaged by Elestio

[Gitness](https://github.com/harness/gitness.git) is an open source development platform packed with the power of code hosting and automated DevOps pipelines.

<img src="https://github.com/elestio-examples/gitness/raw/main/gitness.png" alt="gitness" width="800">

Deploy a <a target="_blank" href="https://elest.io/open-source/gitness">fully managed Gitness</a> on <a target="_blank" href="https://elest.io/">elest.io</a> if you are interested in exploring a decentralized and community-oriented approach to online content.

[![deploy](https://github.com/elestio-examples/gitness/raw/main/deploy-on-elestio.png)](https://dash.elest.io/deploy?soft=gitness)

# Why use Elestio images?

- Elestio stays in sync with updates from the original source and quickly releases new versions of this image through our automated processes.
- Elestio images provide timely access to the most recent bug fixes and features.
- Our team performs quality control checks to ensure the products we release meet our high standards.

# Usage

## Git clone

You can deploy it easily with the following command:

    git clone https://github.com/elestio-examples/gitness.git

Copy the .env file from tests folder to the project directory

    cp ./tests/.env ./.env

Edit the .env file with your own values.

Set env vars

    set -o allexport; source .env; set +o allexport;

Run the project with the following command

    docker-compose up -d

Run below steps after install:

    set -o allexport; source .env; set +o allexport;

    #wait until the server is ready
    echo "Waiting for software to be ready ..."
    sleep 30s;

    target=$(docker-compose port gitness 53521)

    curl http://${target}/api/v1/register?include_cookie=true \
      -H 'accept: */*' \
      -H 'accept-language: fr-FR,fr;q=0.9,en-US;q=0.8,en;q=0.7,he;q=0.6' \
      -H 'authorization;' \
      -H 'cache-control: no-cache' \
      -H 'content-type: application/json' \
      -H 'pragma: no-cache' \
      -H 'user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.0.0 Safari/537.36' \
      --data-raw '{"display_name":"root","email":"'${ADMIN_EMAIL}'","uid":"root","password":"'${ADMIN_PASSWORD}'"}' \
      --compressed

You can access the Web UI at: `http://your-domain:53521`

## Docker-compose

Here are some example snippets to help you get started creating a container.

    version: "3.3"
    services:
      gitness:
        image: elestio4test/gitness:${SOFTWARE_VERSION_TAG}
        restart: always
        ports:
          - "172.17.0.1:53521:53521"
        environment:
          - GITNESS_URL_API=https://${DOMAIN}/api
          - GITNESS_URL_GIT=https://${DOMAIN}/git
          - GITNESS_HTTP_PORT=53521
        volumes:
          - "/var/run/docker.sock:/var/run/docker.sock"
          - "./storage/gitness:/data"

### Environment variables

|       Variable       |       Value (example)      |
| :------------------: | :------------------------: |
|       DOMAIN         |   http://172.17.0.1:53521  |
|     ADMIN_EMAIL      |      test@gmail.com        |
|    ADMIN_PASSWORD    |         test@123           |

# Maintenance

## Logging

The Elestio Gitness Docker image sends the container logs to stdout. To view the logs, you can use the following command:

    docker-compose logs -f

To stop the stack you can use the following command:

    docker-compose down

## Backup and Restore with Docker Compose

To make backup and restore operations easier, we are using folder volume mounts. You can simply stop your stack with docker-compose down, then backup all the files and subfolders in the folder near the docker-compose.yml file.

Creating a ZIP Archive
For example, if you want to create a ZIP archive, navigate to the folder where you have your docker-compose.yml file and use this command:

    zip -r myarchive.zip .

Restoring from ZIP Archive
To restore from a ZIP archive, unzip the archive into the original folder using the following command:

    unzip myarchive.zip -d /path/to/original/folder

Starting Your Stack
Once your backup is complete, you can start your stack again with the following command:

    docker-compose up -d

That's it! With these simple steps, you can easily backup and restore your data volumes using Docker Compose.

# Links

- <a target="_blank" href="https://github.com/harness/gitness">Gitness Github repository</a>

- <a target="_blank" href="https://docs.gitness.com/">Gitness documentation</a>

- <a target="_blank" href="https://github.com/elestio-examples/gitness">Elestio/Gitness Github repository</a>
