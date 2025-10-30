# build stage
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

COPY ["app.csproj", "./"]
RUN dotnet restore

COPY . .

RUN dotnet publish -c Release -o /app/publish

# final stage
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS final
WORKDIR /app

USER $APP_UID

COPY --from=build /app/publish .

EXPOSE 8080

ENTRYPOINT [ "dotnet", "app.dll" ]