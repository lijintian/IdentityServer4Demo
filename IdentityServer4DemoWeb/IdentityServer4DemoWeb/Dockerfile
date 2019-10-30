FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 1719
EXPOSE 44391

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY IdentityServer4DemoWeb/IdentityServer4DemoWeb.csproj IdentityServer4DemoWeb/
RUN dotnet restore IdentityServer4DemoWeb/IdentityServer4DemoWeb.csproj
COPY . .
WORKDIR /src/IdentityServer4DemoWeb
RUN dotnet build IdentityServer4DemoWeb.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish IdentityServer4DemoWeb.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "IdentityServer4DemoWeb.dll"]
