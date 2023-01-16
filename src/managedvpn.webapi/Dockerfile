FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/managedvpn.webapi/managedvpn.webapi.csproj", "src/managedvpn.webapi/"]
RUN dotnet restore "src/managedvpn.webapi/managedvpn.webapi.csproj"
COPY . .
WORKDIR "/src/src/managedvpn.webapi"
RUN dotnet build "managedvpn.webapi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "managedvpn.webapi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "managedvpn.webapi.dll"]
