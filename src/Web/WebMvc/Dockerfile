# RUN BOTH CONTAINERS FROM ROOT (folder with .sln file):
# docker-compose build
# docker-compose up
#
# RUN JUST THIS CONTAINER FROM ROOT (folder with .sln file):
# docker build --pull -t taponto.webmvc -f src/Taponto.WebMvc/Dockerfile .
#
# RUN COMMAND
# docker run --name taponto.webmvc --rm -it -p 5000:5000 taponto.webmvc
FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY Taponto-WebMvc.sln .
COPY src/Taponto.Domain/Taponto.Domain.csproj src/Taponto.Domain/
COPY src/Taponto.WebMvc/Taponto.WebMvc.csproj src/Taponto.WebMvc/
RUN dotnet restore
COPY . .

# copy everything else and build app
WORKDIR /app/src/Taponto.WebMvc
RUN dotnet publish -c Release -o out


FROM mcr.microsoft.com/dotnet/core/aspnet:2.2 AS runtime
WORKDIR /app
COPY --from=build /app/src/Taponto.WebMvc/out ./

# Optional: Set this here if not setting it from docker-compose.yml
# ENV ASPNETCORE_ENVIRONMENT Development

ENTRYPOINT ["dotnet", "Taponto.WebMvc.dll"]
