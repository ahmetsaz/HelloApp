# HelloApp
There is a Dockerfile for .net core 3.1 in the application.
I used github action for the Docker file CI process. You can check the action.yml file in the .github/workflows/ file. I sent the generated image in ahmetsaz/helloapp.
To run the Docker Image:

docker pull ahmetsaz/helloapp:latest
docker run -p 11130:11130 ahmetsaz/helloapp:latest

I used Azure for Kubernetes cluster environment

