﻿FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /app
COPY . ./
RUN dotnet restore ./AspNetGha.csproj
RUN dotnet build AspNetGha.csproj -c $BUILD_CONFIGURATION -o /app/build
RUN dotnet publish "AspNetGha.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
USER $APP_UID
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "AspNetGha.dll"]
