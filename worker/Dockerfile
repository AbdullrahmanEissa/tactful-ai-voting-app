FROM mcr.microsoft.com/dotnet/sdk:7.0-alpine AS build
WORKDIR /src
COPY Worker.csproj .
RUN dotnet restore Worker.csproj
COPY . .
WORKDIR "/src"
RUN dotnet build Worker.csproj -c Release -o /app/build

FROM mcr.microsoft.com/dotnet/runtime-deps:7.0-alpine AS final
WORKDIR /app
COPY --from=build /app/build .
# Since it's a self-contained or needs runtime, but runtime-deps is very light.
# Let's use runtime for simplicity or publish as self-contained.
# Actually, let's use the runtime image to be safe and light.
FROM mcr.microsoft.com/dotnet/runtime:7.0-alpine
WORKDIR /app
COPY --from=build /app/build .
ENTRYPOINT ["dotnet", "Worker.dll"]