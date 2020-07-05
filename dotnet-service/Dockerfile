# Stage 1: Build project into
FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /source

COPY *.csproj .
RUN dotnet restore

COPY . .
RUN dotnet build
RUN dotnet publish -c release -o /app --no-restore

# Stage 2: run project
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
WORKDIR /app
EXPOSE 80

COPY --from=build /app .
ENTRYPOINT ["dotnet", "dotnet-service.dll"]