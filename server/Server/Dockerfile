# File: Abbsium-web/server/Server/Dockerfile

# Stage 1: Base runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

# Stage 2: Build
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src

# Copy only the .csproj first to optimize layer caching
COPY Server.csproj ./

# Restore packages
RUN dotnet restore

# Now copy the rest of the project files
COPY . . 

# Publish the project
RUN dotnet publish -c Release -o /app/publish

# Stage 3: Final runtime image
FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .

ENTRYPOINT ["dotnet", "Server.dll"]
