# RUN JUST THIS CONTAINER FROM ROOT (folder with .sln file):
# docker build --pull -t taponto.unittest -f tests/UnitTests/Dockerfile .
#
# RUN COMMAND
# docker run --name taponto.unittest --rm taponto.unittest
FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build
WORKDIR /test

# copy csproj and restore as distinct layers
COPY Taponto.sln ./
COPY tests/UnitTests/UnitTests.csproj tests/UnitTests/
COPY src/Taponto.Domain/Taponto.Domain.csproj src/Taponto.Domain/
COPY src/Taponto.WebMvc/Taponto.WebMvc.csproj src/Taponto.WebMvc/
RUN dotnet restore
COPY . .

WORKDIR /test/tests/UnitTests
RUN dotnet build -c Release 
ENTRYPOINT ["dotnet", "test", "-c","Release", "--logger:trx"]