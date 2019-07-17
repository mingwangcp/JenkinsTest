FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 8080

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["DockerWeb_Test/DockerWeb_Test.csproj", "DockerWeb_Test/"]
RUN dotnet restore "DockerWeb_Test/DockerWeb_Test.csproj"
COPY . .
WORKDIR "/src/DockerWeb_Test"
RUN dotnet build "DockerWeb_Test.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DockerWeb_Test.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerWeb_Test.dll"]