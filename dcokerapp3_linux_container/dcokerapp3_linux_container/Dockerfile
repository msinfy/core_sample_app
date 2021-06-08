FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["dcokerapp3_linux_container/dcokerapp3_linux_container.csproj", "dcokerapp3_linux_container/"]
RUN dotnet restore "dcokerapp3_linux_container/dcokerapp3_linux_container.csproj"
COPY . .
WORKDIR "/src/dcokerapp3_linux_container"
RUN dotnet build "dcokerapp3_linux_container.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dcokerapp3_linux_container.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dcokerapp3_linux_container.dll"]