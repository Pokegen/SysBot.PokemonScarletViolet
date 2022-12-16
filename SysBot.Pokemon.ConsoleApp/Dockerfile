FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["SysBot.Pokemon.ConsoleApp/SysBot.Pokemon.ConsoleApp.csproj", "SysBot.Pokemon.ConsoleApp/"]
RUN dotnet restore "SysBot.Pokemon.ConsoleApp/SysBot.Pokemon.ConsoleApp.csproj"
COPY . .
WORKDIR "/src/SysBot.Pokemon.ConsoleApp"
RUN dotnet build "SysBot.Pokemon.ConsoleApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SysBot.Pokemon.ConsoleApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
RUN apt update && apt install z3
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SysBot.Pokemon.ConsoleApp.dll"]