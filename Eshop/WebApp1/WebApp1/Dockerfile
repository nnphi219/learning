#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["WebApp1/WebApp1/WebApp1.csproj", "WebApp1/"]
RUN dotnet restore "WebApp1/WebApp1.csproj"
COPY . .
WORKDIR "/src/WebApp1/WebApp1"
RUN dotnet build "WebApp1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApp1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApp1.dll"]