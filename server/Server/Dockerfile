# Dockerfile located in Abbsium-web/server/Server/
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src # This will be /src inside the container

# Copy everything from the current build context (Abbsium-web/server/Server/)
# directly into /src in the container.
COPY . .

# Restore dependencies. dotnet restore should find Server.csproj directly in /src.
RUN dotnet restore

# Publish the application.
RUN dotnet publish -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "Server.dll"]