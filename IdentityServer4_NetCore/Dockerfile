FROM microsoft/dotnet:2.2-aspnetcore-runtime-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk-stretch AS build
WORKDIR /src
COPY ["IdentityServer4_NetCore/IdentityServer4_NetCore.csproj", "IdentityServer4_NetCore/"]
RUN dotnet restore "IdentityServer4_NetCore/IdentityServer4_NetCore.csproj"
COPY . .
WORKDIR "/src/IdentityServer4_NetCore"
RUN dotnet build "IdentityServer4_NetCore.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "IdentityServer4_NetCore.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "IdentityServer4_NetCore.dll"]