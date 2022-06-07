#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["AzWebApi/AzWebApi.csproj", "AzWebApi/"]
RUN dotnet restore "AzWebApi/AzWebApi.csproj"
COPY . .
WORKDIR "/src/AzWebApi"
RUN dotnet build "AzWebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AzWebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AzWebApi.dll"]