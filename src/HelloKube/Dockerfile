FROM microsoft/dotnet:2.2-sdk-alpine AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY HelloKube.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/dotnet:2.2.0-aspnetcore-runtime-alpine
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "HelloKube.dll"]