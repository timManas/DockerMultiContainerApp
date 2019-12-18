# DockerMultiContainerApp

Steps
1. Copy over package.json
2. Run npm install
3. Copy over everything else
4. Docker compose should set up volume to share files


How to execute on Client
docker build -f Dockerfile.dev .
docker run <imageid>

Inside DockerCompose file we should
Postrgres:
    - What image to use ?
Redis:
    - What image to use ?
Server:
    - Specify which build
    - Specify volume
    - Specify Env variables


Note
1. Docker-compose.yml file is created in the root directory

How to execute docker-compose
> docker-compose up --build


What does default.conf do ?
1. Tell Nginx that there is a client upstream server at client:3000
2. Tell Nginx that there is a client upstream server at server:5000
3. List on Port 80
4. If anyone comes to '/' send them client upstream
5. If anyone coems to '/api' send them to server upstream


How to push code to DockerHub ? 
- you need to be login
> docker login

- Create a travis YAML file which does the following 
after_success:
    - docker build -t timmanas/multi-client ./client
    - docker build -t timmanas/multi-nginx ./nginx
    - docker build -t timmanas/multi-server ./server
    - docker build -t timmanas/multi-worker ./worker
    
    # Log in to the DOCKER CLI
    # What does this do ? It performs login in automatically without user intervention
    - echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_ID" --password-stdin

    # Take those images and push them to docker hub 
    - docker push timmanas/multi-client
    - docker push timmanas/multi-nginx
    - docker push timmanas/multi-server
    - docker push timmanas/multi-worker