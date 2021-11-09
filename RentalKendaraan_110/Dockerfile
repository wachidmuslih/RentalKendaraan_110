#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["RentalKendaraan_110/RentalKendaraan_110.csproj", "RentalKendaraan_110/"]
RUN dotnet restore "RentalKendaraan_110/RentalKendaraan_110.csproj"
COPY . .
WORKDIR "/src/RentalKendaraan_110"
RUN dotnet build "RentalKendaraan_110.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RentalKendaraan_110.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RentalKendaraan_110.dll"]