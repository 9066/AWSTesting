FROM microsoft/dotnet:3.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:3.1-sdk AS build 
WORKDIR /src
COPY ["AWSTesting.csproj", "AWSTesting/"]
RUN dotnet restore "AWSTesting/AwsService.csproj"
COPY . "AWSTesting/"
WORKDIR "/src/AWSTesting"
RUN dotnet build "AWSTesting.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AWSTesting.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AWSTesting.dll"] 

