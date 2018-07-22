FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY Muzyk/Muzyk.csproj Muzyk/
RUN dotnet restore Muzyk/Muzyk.csproj
COPY . .
WORKDIR /src/Muzyk
RUN dotnet build Muzyk.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Muzyk.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Muzyk.dll"]
