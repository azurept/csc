FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
LABEL stage=build
WORKDIR /src
COPY . .
RUN dotnet restore "WeatherApi.csproj"
RUN dotnet build "WeatherApi.csproj" -c Release -o /app/build
RUN dotnet publish "WeatherApi.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS final
WORKDIR /app
ENV ASPNETCORE_URLS http://+:9000
EXPOSE 9000
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "WeatherApi.dll"]
