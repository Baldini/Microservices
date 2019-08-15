FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["src/Order.API/Order.API.csproj", "src/Order.API/"]
RUN dotnet restore "src/Order.API/Order.API.csproj"
COPY . .
WORKDIR "/src/src/Order.API"
RUN dotnet build "Order.API.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Order.API.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Order.API.dll"]
