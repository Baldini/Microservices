FROM mcr.microsoft.com/dotnet/core/runtime:2.2-stretch-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["src/Order.Orchestrator/Order.Orchestrator.csproj", "src/Order.Orchestrator/"]
RUN dotnet restore "src/Order.Orchestrator/Order.Orchestrator.csproj"
COPY . .
WORKDIR "/src/src/Order.Orchestrator"
RUN dotnet build "Order.Orchestrator.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Order.Orchestrator.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Order.Orchestrator.dll"]
