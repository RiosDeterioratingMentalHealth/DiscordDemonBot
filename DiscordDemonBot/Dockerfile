# https://hub.docker.com/_/microsoft-dotnet
FROM mcr.microsoft.com/dotnet/sdk:7.0-jammy AS build
WORKDIR /source

# copy csproj and restore as distinct layers
COPY *.csproj .
RUN dotnet restore -r linux-arm64

# copy and publish app and libraries
COPY . .
RUN dotnet publish -c Release -o /app -r linux-arm64 --self-contained true --no-restore

# final stage/image
FROM mcr.microsoft.com/dotnet/runtime:7.0-jammy-arm64v8
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["./DiscordDemonBot"]
