#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 5000

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["dockerdemo1/dockerdemo1.csproj", "dockerdemo1/"]
RUN dotnet restore "dockerdemo1/dockerdemo1.csproj"
COPY . .
WORKDIR "/src/dockerdemo1"
RUN dotnet build "dockerdemo1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dockerdemo1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dockerdemo1.dll"]