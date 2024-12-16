FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["YazilimAcademy.WebApi/YazilimAcademy.WebApi.csproj", "YazilimAcademy.WebApi/"]
RUN dotnet restore "YazilimAcademy.WebApi/YazilimAcademy.WebApi.csproj"
COPY . .
WORKDIR "/src/YazilimAcademy.WebApi"
RUN dotnet build "YazilimAcademy.WebApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "YazilimAcademy.WebApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "YazilimAcademy.WebApi.dll"]
