FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["ServiceApiOrder/ServiceApiOrder.csproj", "ServiceApiOrder/"]
RUN dotnet restore "ServiceApiOrder/ServiceApiOrder.csproj"
COPY . .
WORKDIR "/src/ServiceApiOrder"
RUN dotnet build "ServiceApiOrder.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ServiceApiOrder.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ServiceApiOrder.dll"]