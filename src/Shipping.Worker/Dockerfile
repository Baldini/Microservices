FROM mcr.microsoft.com/dotnet/core/runtime:2.2-stretch-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["src/Shipping.Worker/Shipping.Worker.csproj", "src/Shipping.Worker/"]
RUN dotnet restore "src/Shipping.Worker/Shipping.Worker.csproj"
COPY . .
WORKDIR "/src/src/Shipping.Worker"
RUN dotnet build "Shipping.Worker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Shipping.Worker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Shipping.Worker.dll"]
