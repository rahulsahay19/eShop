#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Client/StatusCheck/StatusCheck.csproj", "Client/StatusCheck/"]
RUN dotnet restore "Client/StatusCheck/StatusCheck.csproj"
COPY . .
WORKDIR "/src/Client/StatusCheck"
RUN dotnet build "StatusCheck.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "StatusCheck.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "StatusCheck.dll"]
