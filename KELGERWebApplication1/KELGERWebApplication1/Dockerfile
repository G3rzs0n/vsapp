#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["KELGERWebApplication1/KELGERWebApplication1.csproj", "KELGERWebApplication1/"]
RUN dotnet restore "KELGERWebApplication1/KELGERWebApplication1.csproj"
COPY . .
WORKDIR "/src/KELGERWebApplication1"
RUN dotnet build "KELGERWebApplication1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "KELGERWebApplication1.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "KELGERWebApplication1.dll"]