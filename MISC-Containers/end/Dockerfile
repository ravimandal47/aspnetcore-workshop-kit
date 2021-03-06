# Describes how to build a Docker image. Each instruction creates a new layer in the image. 

# base image
# This has the SDK installed; I don't think it used to. 
#FROM microsoft/dotnet:latest
# I am not sure what is unique to this image vs the one above
FROM microsoft/dotnet:1.0.0-preview2-sdk
# This is good for deployed apps as it will be minimal, and no SDK 
#FROM microsoft/dotnet:1.0.1-core 

# set up network
EXPOSE 5000/tcp
ENV ASPNETCORE_URLS http://*:5000

# copy files from current directory to target on container - i.e. if you want your app in the container and want to deploy it
# COPY . /sampleAspnetCoreWebApiApp 
# WORKDIR /sampleAspnetCoreWebApiApp

RUN ["dotnet", "restore"]
RUN ["dotnet", "build"]
ENTRYPOINT ["dotnet", "watch", "run"]

# USAGE - build image, and expose ports, the current app folder: 
# 		docker build -t mydemos:aspnetcorehelloworld .
#		docker run -d -p 8080:5000 -v $(pwd):/app -t mydemos:aspnetcorehelloworld 

# REFERENCE: https://github.com/aspnet/aspnet-docker/blob/master/1.0.1/jessie/product/Dockerfile


#------------------------
# FOR MULTIPLE CONTAINERS
# docker build -f aspnetcore.development.dockerfile -t [yourDockerHubID]/dotnet:1.0.0 

# Option 1
# Start PostgreSQL and ASP.NET Core (link ASP.NET core to ProgreSQL container with legacy linking)
 
# docker run -d --name my-postgres -e POSTGRES_PASSWORD=password postgres
# docker run -d -p 5000:5000 --link my-postgres:postgres [yourDockerHubID]/dotnet:1.0.0

# Option 2: Create a custom bridge network and add containers into it

# docker network create --driver bridge isolated_network
# docker run -d --net=isolated_network --name postgres -e POSTGRES_PASSWORD=password postgres
# docker run -d --net=isolated_network --name aspnetcoreapp -p 5000:5000 [yourDockerHubID]/dotnet:1.0.0