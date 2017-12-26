FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY *.sln ./
COPY Sagas.Service.A/Sagas.Service.A.csproj Sagas.Service.A/
RUN dotnet restore
COPY . .
WORKDIR /src/Sagas.Service.A
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Sagas.Service.A.dll"]
