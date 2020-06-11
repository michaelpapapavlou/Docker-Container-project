#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Docker Container project/Docker Container project.csproj", "Docker Container project/"]
RUN dotnet restore "Docker Container project/Docker Container project.csproj"
COPY . .
WORKDIR "/src/Docker Container project"
RUN dotnet build "Docker Container project.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Docker Container project.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Docker Container project.dll"]