FROM microsoft/aspnetcore:2.2 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.2 AS build
WORKDIR /src
COPY *.sln ./
COPY challengerGit/challengerGit.csproj challengerGit/
RUN dotnet restore
COPY . .
WORKDIR /src/challengerGit
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "challengerGit.dll"]
