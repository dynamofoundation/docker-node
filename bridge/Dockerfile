# syntax=docker/dockerfile:1
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build-env
WORKDIR /app

RUN apt-get update && \
    apt-get install -y git && \
    git clone https://github.com/dynamofoundation/web-app-server.git && \
    mv web-app-server/web-app-server/* . 


# Copy csproj and restore as distinct layers
#COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
#COPY ../engine/examples ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:3.1
WORKDIR /app
COPY settings.txt .
#RUN ls -1
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "web-app-server.dll"]

