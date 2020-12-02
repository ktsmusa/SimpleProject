#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["SimpleProject/SimpleProject.csproj", "SimpleProject/"]
RUN dotnet restore "SimpleProject/SimpleProject.csproj"
COPY . .
WORKDIR "/src/SimpleProject"
RUN dotnet build "SimpleProject.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SimpleProject.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SimpleProject.dll"]