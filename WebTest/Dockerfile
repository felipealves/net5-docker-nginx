FROM mcr.microsoft.com/dotnet/sdk:5.0-alpine AS base
WORKDIR /app
ENV ASPNETCORE_URLS=http://+:5000  
ENV ASPNETCORE_ENVIRONMENT=Development
EXPOSE 5000

FROM mcr.microsoft.com/dotnet/sdk:5.0-alpine AS build
WORKDIR /source
COPY . .
RUN dotnet restore 
RUN dotnet build --no-restore -c Release -o /app

FROM build AS publish
RUN dotnet publish --no-restore -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .

# Padrão de container ASP.NET
ENTRYPOINT ["dotnet", "WebTest.dll"]