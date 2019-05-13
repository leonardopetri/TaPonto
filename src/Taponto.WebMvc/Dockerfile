# RUN BOTH CONTAINERS FROM ROOT (folder with .sln file):
# docker-compose build
# docker-compose up
#
# RUN JUST THIS CONTAINER FROM ROOT (folder with .sln file):
# docker build --pull -t taponto.webmvc -f src/Taponto.WebMvc/Dockerfile .
#
# RUN COMMAND
# docker run --name taponto.webmvc --rm -it -p 5107:5107 taponto.webmvc
FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY *.sln .
COPY . .
RUN dotnet restore

# copy everything else and build app
WORKDIR /app/src/Taponto.WebMvc
RUN dotnet publish -c Release -o out


FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS runtime
WORKDIR /app
COPY --from=build /app/src/Taponto.WebMvc/out ./

# Optional: Set this here if not setting it from docker-compose.yml
# ENV ASPNETCORE_ENVIRONMENT Development

ENTRYPOINT ["dotnet", "Taponto.WebMvc.dll"]
