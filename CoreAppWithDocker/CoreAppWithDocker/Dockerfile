FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["CoreAppWithDocker/CoreAppWithDocker.csproj", "CoreAppWithDocker/"]
RUN dotnet restore "CoreAppWithDocker/CoreAppWithDocker.csproj"
COPY . .
WORKDIR "/src/CoreAppWithDocker"
RUN dotnet build "CoreAppWithDocker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CoreAppWithDocker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CoreAppWithDocker.dll"]