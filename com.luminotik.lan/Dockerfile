#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["com.luminotik.lan/com.luminotik.lan.csproj", "com.luminotik.lan/"]
RUN dotnet restore "com.luminotik.lan/com.luminotik.lan.csproj"
COPY . .
WORKDIR "/src/com.luminotik.lan"
RUN dotnet build "com.luminotik.lan.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "com.luminotik.lan.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "com.luminotik.lan.dll"]