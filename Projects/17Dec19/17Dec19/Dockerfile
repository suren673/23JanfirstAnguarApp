FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY 17Dec19/17Dec19.csproj 17Dec19/
RUN dotnet restore "17Dec19/17Dec19.csproj"
COPY . .
WORKDIR "/src/17Dec19"
RUN dotnet build "17Dec19.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "17Dec19.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "17Dec19.dll"]
