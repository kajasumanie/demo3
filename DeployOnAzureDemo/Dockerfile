FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["DeployOnAzureDemo/DeployOnAzureDemo.csproj", "DeployOnAzureDemo/"]
RUN dotnet restore "DeployOnAzureDemo/DeployOnAzureDemo.csproj"
COPY . .
WORKDIR "/src/DeployOnAzureDemo"
RUN dotnet build "DeployOnAzureDemo.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "DeployOnAzureDemo.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DeployOnAzureDemo.dll"]