FROM mcr.microsoft.com/dotnet/core/runtime:3.1-buster-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY AgileSqlClub.SqlPackageFilter.Core.csproj .
RUN dotnet restore "AgileSqlClub.SqlPackageFilter.Core.csproj"
COPY . .
RUN dotnet build "AgileSqlClub.SqlPackageFilter.Core.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "AgileSqlClub.SqlPackageFilter.Core.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["/bin/bash"]