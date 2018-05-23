FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY src/Test/Test.csproj src/Test/
RUN dotnet restore src/Test/Test.csproj
COPY . .
WORKDIR /src/src/Test
RUN dotnet build Test.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Test.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Test.dll"]
