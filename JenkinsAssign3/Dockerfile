# Use the official ASP.NET runtime as a parent image
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

# Use the official .NET SDK image to build the app
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["/JenkinsAssign3.csproj", "/"]
RUN dotnet restore "/JenkinsAssign3.csproj"
COPY . .
WORKDIR "/src/"
RUN dotnet build "JenkinsAssign3.csproj" -c Release -o /app/build

# Publish the app
FROM build AS publish
RUN dotnet publish "JenkinsAssign3.csproj" -c Release -o /app/publish /p:UseAppHost=false

# Use the ASP.NET runtime image to run the app
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "JenkinsAssign3.dll"]
