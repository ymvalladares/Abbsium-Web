# Usa imagen base oficial de .NET SDK
# Stage 1: Base runtime image for the final application
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

# Stage 2: Build the application using the SDK image
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy the server solution and project file(s) first.
# This assumes you will run 'docker build' from the 'Abbsium-web' root.
# We copy the entire 'server' folder from the build context.
COPY ["server/", "server/"]

# Set the working directory to the specific project folder where Server.csproj resides.
# This is crucial for dotnet restore to find the file.
WORKDIR /src/server/Server
RUN dotnet restore

# Copy the rest of your application code to the current working directory (/src/server/Server).
COPY . .

# Publish the application.
# The output will be in /app/publish inside this build stage.
RUN dotnet publish -c Release -o /app/publish

# Stage 3: Final runtime image
FROM base AS final
WORKDIR /app
# Copy the published application from the build stage to the final stage.
COPY --from=build /app/publish .
# Set the entrypoint for your application.
ENTRYPOINT ["dotnet", "Server.dll"]
