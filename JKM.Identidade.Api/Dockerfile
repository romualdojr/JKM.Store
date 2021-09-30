#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["JKM.Identidade.Api/JKM.Identidade.Api.csproj", "JKM.Identidade.Api/"]
RUN dotnet restore "JKM.Identidade.Api/JKM.Identidade.Api.csproj"
COPY . .
WORKDIR "/src/JKM.Identidade.Api"
RUN dotnet build "JKM.Identidade.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "JKM.Identidade.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "JKM.Identidade.Api.dll"]