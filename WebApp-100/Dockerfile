#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["WebApp-100/WebApp-100.csproj", "WebApp-100/"]
RUN dotnet restore "WebApp-100/WebApp-100.csproj"
COPY . .
WORKDIR "/src/WebApp-100"
RUN dotnet build "WebApp-100.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WebApp-100.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WebApp-100.dll"]