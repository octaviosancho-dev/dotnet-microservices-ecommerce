# Etapa de construcci�n
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env
WORKDIR /app

# Copiar el archivo .csproj espec�fico y restaurar dependencias
COPY ./FoodDelivery.Services.CouponAPI.csproj ./
RUN dotnet restore "./FoodDelivery.Services.CouponAPI.csproj"

# Copiar todo el resto del c�digo del microservicio
COPY ./ ./

# Compilar y publicar el c�digo
WORKDIR /app
RUN dotnet publish -c Release -o out

# Etapa de runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build-env /app/out .

# Exponer puerto
EXPOSE 7001

# Ejecutar la aplicaci�n
ENTRYPOINT ["dotnet", "FoodDelivery.Services.CouponAPI.dll"]