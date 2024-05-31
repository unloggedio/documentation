# Deploying the server

## Creating an S3 bucket and getting environment variables
- Create a private S3 bucket in AWS.
- To use the server following environment variables are needed:
    - `bucket_name`: Name of s3 bucket
    - `bucket_region_url`: This is the URL of s3 region. For example [`https://s3.eu-west-1.amazonaws.com`](https://s3.eu-west-1.amazonaws.com/)
    - `bucket_region`: This is region of S3 bucket. For example: `eu-west-1`.
    - To get the `access_key` and `secret_key` go to the security credentials of you account and create an access key.

## Deploying the server
- Deploying the server can happen through docker or jar file.

### Deployment by docker container

- To deploy the server from docker run the following commands:

```bash
# create a docker volume 
docker volume create unlogged_volume

# run the docker container
docker run -dp 8123:8123 
-v unlogged_volume:/usr/src/app/local-session 
-e cloud.bucketName=bucket_name
-e cloud.endpoint=bucket_region_url
-e cloud.aws.region.static=bucket_region
-e cloud.aws.credentials.access-key=access_key
-e cloud.aws.credentials.secret-key=secret_key
public.ecr.aws/z6h2b9v3/unlogged_server:latest
```

### Deployment by docker-compose

- The server can be deployed using docker compose. An example docker-compose file is as follows:

```docker
version: '2'

services:
  unlogged_server:
    image: public.ecr.aws/z6h2b9v3/unlogged_server:latest
    ports:
      - "8123:8123"
    volumes:
      - unlogged_volume:/usr/src/app/local-session
    environment:
      - cloud.bucketName=bucket_name
      - cloud.endpoint=bucket_region_url
      - cloud.aws.region.static=bucket_region
      - cloud.aws.credentials.access-key=access_key
      - cloud.aws.credentials.secret-key=secret_key

volumes:
  unlogged_volume:
    external: true
```

- Create a volume using `docker volume create unlogged_volume`
- Run the container using `docker compose -f path_to_file up -d`

### Deployment from JAR

- To deploy the service using jar use the following command:
    
    ```bash
    java -jar -Dcloud.bucketName=bucket_name \
    	-Dcloud.endpoint=bucket_region_url \
    	-Dcloud.aws.region.static=bucket_region \
    	-Dcloud.aws.credentials.access-key=access_key \
    	-Dcloud.aws.credentials.secret-key=secret_key \
    	unlogged_server.jar
    ```
    

## Verifying the status of deployed service

- If deployed on local machine go to `http://localhost:8123/session/ping`
- If deployed on an EC2 instance go to `http://public_ip:8123/session/ping`
