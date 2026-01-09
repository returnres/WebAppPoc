FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["WebAppBlazorS/WebAppBlazorS.csproj", "WebAppBlazorS/"]
RUN dotnet restore "WebAppBlazorS/WebAppBlazorS.csproj"
COPY . .
WORKDIR "/src/WebAppBlazorS"
RUN dotnet build "WebAppBlazorS.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "WebAppBlazorS.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebAppBlazorS.dll"]
