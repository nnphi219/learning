#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["Web.Api1/Web.Api1.csproj", "Web.Api1/"]
RUN dotnet restore "Web.Api1/Web.Api1.csproj"
COPY . .
WORKDIR "/src/Web.Api1"
RUN dotnet build "Web.Api1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Web.Api1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Web.Api1.dll"]