FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["IISI-2209026/IISI_2209026.csproj", "IISI-2209026/"]
RUN dotnet restore "IISI-2209026/IISI_2209026.csproj"
COPY . .
WORKDIR "/src/IISI-2209026"
RUN dotnet build "IISI_2209026.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "IISI_2209026.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM nginx AS final
EXPOSE 80
WORKDIR /usr/share/nginx/html
COPY --from=publish /app/publish/wwwroot .