FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 3928
EXPOSE 44362

FROM microsoft/dotnet:2.1-sdk-nanoserver-1709 AS build
WORKDIR /src
COPY Docker/Docker.csproj Docker/
RUN dotnet restore Docker/Docker.csproj
COPY . .
WORKDIR /src/Docker
RUN dotnet build Docker.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Docker.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Docker.dll"]
