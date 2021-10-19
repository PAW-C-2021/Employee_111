#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["Employee_111/Employee_111.csproj", "Employee_111/"]
RUN dotnet restore "Employee_111/Employee_111.csproj"
COPY . .
WORKDIR "/src/Employee_111"
RUN dotnet build "Employee_111.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Employee_111.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Employee_111.dll"]