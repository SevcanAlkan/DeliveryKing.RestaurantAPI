#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["DeliveryKing.RestaurantAPI/DeliveryKing.RestaurantAPI.csproj", "DeliveryKing.RestaurantAPI/"]
RUN dotnet restore "DeliveryKing.RestaurantAPI/DeliveryKing.RestaurantAPI.csproj"
COPY . .
WORKDIR "/src/DeliveryKing.RestaurantAPI"
RUN dotnet build "DeliveryKing.RestaurantAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DeliveryKing.RestaurantAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DeliveryKing.RestaurantAPI.dll"]