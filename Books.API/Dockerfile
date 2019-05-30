FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["Books.API/Books.API.csproj", "Books.API/"]
RUN dotnet restore "Books.API/Books.API.csproj"
COPY . .
WORKDIR "/src/Books.API"
RUN dotnet build "Books.API.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Books.API.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Books.API.dll"]