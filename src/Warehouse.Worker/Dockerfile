FROM mcr.microsoft.com/dotnet/core/runtime:2.2-stretch-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["src/Warehouse.Worker/Warehouse.Worker.csproj", "src/Warehouse.Worker/"]
RUN dotnet restore "src/Warehouse.Worker/Warehouse.Worker.csproj"
COPY . .
WORKDIR "/src/src/Warehouse.Worker"
RUN dotnet build "Warehouse.Worker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Warehouse.Worker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Warehouse.Worker.dll"]
