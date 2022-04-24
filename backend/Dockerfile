### SDK -> https://hub.docker.com/_/microsoft-dotnet-sdk
### ============================================================================
FROM mcr.microsoft.com/dotnet/sdk as build

WORKDIR /backend
COPY backend.csproj .
RUN dotnet restore

COPY . .
RUN dotnet publish -c Release -o /backend-release

### ASP.NET RUNTIME
### ============================================================================
FROM mcr.microsoft.com/dotnet/aspnet AS runtime

### COPY PUBLISHED APP
WORKDIR /app
COPY --from=build /backend-release .

### TIME ZONE
ENV TZ=Europe/Berlin

### CREATE BUILD INFO FILE (MUST COME AFTER THE APP COPY)
#WORKDIR /app/App_Data
#RUN date '+{"date":"%d.%m.%Y","time":"%H:%M:%S"}' > docker.buildinfo.json

### LANGUAGE
#ENV LANG de_DE.UTF-8
#ENV LANGUAGE ${LANG}
#ENV LC_ALL ${LANG}

### START SETTINGS
EXPOSE 80
ENV ASPNETCORE_URLS=http://+:80
ENV ConnectionStrings__Backend="Server=mySqlServer;Port=3306;User ID=myDbUser;Password=myDbPassword;Database=myDb"

WORKDIR /app
ENTRYPOINT ["dotnet", "backend.dll"]
