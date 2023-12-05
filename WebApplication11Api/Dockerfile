FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/aspnet:8.0.0-jammy AS base
ARG TARGETARCH
USER $APP_UID
WORKDIR /app
EXPOSE 8080
EXPOSE 8081

FROM --platform=$BUILDPLATFORM mcr.microsoft.com/dotnet/sdk:8.0.100-jammy AS build
ARG TARGETARCH
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["WebApplication11Api/WebApplication11Api.csproj", "WebApplication11Api/"]
RUN dotnet restore "WebApplication11Api/WebApplication11Api.csproj" -a $TARGETARCH
COPY . .
WORKDIR "/src/WebApplication11Api"
RUN dotnet build "WebApplication11Api.csproj" -a $TARGETARCH -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "WebApplication11Api.csproj" -a $TARGETARCH --no-restore -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApplication11Api.dll"]
