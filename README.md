# conversao-peso


Dockerfile

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /app
COPY *.csproj .
RUN dotnet restore
COPY . .
RUN dotnet publish -c release -o /app --no-restore


FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
COPY --from=build /app .
EXPOSE 80
EXPOSE 443
ENTRYPOINT ["dotnet", "ConversaoPeso.Web.dll"]


docker image build -t teclinux/conversao-peso:v1 .

docker container run -d -p 5000:80 teclinux/conversao-peso:v1