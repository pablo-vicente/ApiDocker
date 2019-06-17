FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["ApiDocker/ApiDocker.csproj", "ApiDocker/"]
RUN dotnet restore "ApiDocker/ApiDocker.csproj"
COPY . .
WORKDIR "/src/ApiDocker"
RUN dotnet build "ApiDocker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ApiDocker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ApiDocker.dll"]