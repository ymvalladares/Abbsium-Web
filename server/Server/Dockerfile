# Stage 1: Runtime base
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

# Stage 2: Build
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src

# Copiamos todo (Docker ya está en la carpeta correcta)
COPY . .

# Restauramos dependencias
RUN dotnet restore

# Publicamos la app
RUN dotnet publish -c Release -o /app/publish

# Stage 3: Final image
FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .

ENTRYPOINT ["dotnet", "Server.dll"]
