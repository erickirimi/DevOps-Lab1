FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["Lab.Client.Service.csproj", "Lab.Client.Service/"]
RUN dotnet restore "Lab.Client.Service/Lab.Client.Service.csproj"
COPY . .
WORKDIR "/src/Lab.Client.Service"
RUN dotnet build "Lab.Client.Service.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Lab.Client.Service.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Lab.Client.Service.dll"]
