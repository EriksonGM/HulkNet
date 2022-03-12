#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/HulkNet.Dash/HulkNet.Dash.csproj", "src/HulkNet.Dash/"]
RUN dotnet restore "src/HulkNet.Dash/HulkNet.Dash.csproj"
COPY . .
WORKDIR "/src/src/HulkNet.Dash"
RUN dotnet build "HulkNet.Dash.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HulkNet.Dash.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HulkNet.Dash.dll"]