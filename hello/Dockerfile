FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["hello/hello.csproj", "hello/"]
RUN dotnet restore "hello/hello.csproj"
COPY . .
WORKDIR "/src/hello"
RUN dotnet build "hello.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "hello.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "hello.dll"]
