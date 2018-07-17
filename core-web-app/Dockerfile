FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 53497
EXPOSE 44366

FROM microsoft/dotnet:2.1-sdk-nanoserver-1709 AS build
WORKDIR /src
COPY core-web-app/core-web-app.csproj core-web-app/
RUN dotnet restore core-web-app/core-web-app.csproj
COPY . .
WORKDIR /src/core-web-app
RUN dotnet build core-web-app.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish core-web-app.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "core-web-app.dll"]
