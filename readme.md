# EXAMEN DOCKER

**Prestashop** restaShop es una plataforma de comercio electrónico de código abierto que
permite a las empresas y personas crear tiendas en línea.
Es una solución completa y flexible para la creación y gestión de tiendas en línea,
lo que lo convierte en una opción popular para pequeñas y medianas empresas
que desean vender productos y servicios en Internet.


### CREACIÓN DOCKER-COMPOSE.YML
Al crear el fichero *.yml* escribimos el código para definir
la configuración necesaria y ejecutar **Prestashop**:

```
version: '3.3'
services:
  db_prestashop:
    image: mysql:5.7
    ports:
      - "3307:3306"
    volumes:
      - db_data:/var/lib/mysql

    environment:
      - MYSQL_ROOT_PASSWORD=prestashop
      - MYSQL_DATABASE=prestashop
      - MYSQL_USER=prestashop
      - MYSQL_PASSWORD=prestashop

  presta:
    depends_on:
      - db_prestashop
    image: prestashop/prestashop:latest
    ports:
      - "8080:80"
    volumes:
      - './web:/var/www/html'
    environment:
      DB_SERVER: db_prestashop
      DB_USER: prestashop
      DB_PASSWORD: prestashop
      DB_NAME: prestashop
volumes:
  db_data: {}
```