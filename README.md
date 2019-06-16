# nginx-tools
Herramientas para configurar facilmente dominios http y https en nginx Ubuntu

## Prerequisitos 
1. Intalar Ngnix: <https://ubunlog.com/nginx-instala-servidor-ubuntu/>
```sh
$ sudo apt update
$ sudo apt install nginx
```
2. Instalar certbot: <https://certbot.eff.org/lets-encrypt/ubuntubionic-nginx>
```sh
$ sudo apt-get update
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository universe
$ sudo add-apt-repository ppa:certbot/certbot
$ sudo apt-get update
$ sudo apt-get install certbot python-certbot-nginx 
```
## Instalación
Clonar o Descargar este repositorio y ejecutar install.sh
```sh
  ./install.sh
```
**Nota:** Debes asegurarte de haber configurado correctamente el dns de tu dominio para que apunte a tu servidor.
# Comandos
**Nota:** Para que los cambios en la configuración tengan efecto deben estar habilitados.

## ngx-reload:
### Recargar configuración para aplicar cambios:
```sh
  ngx-reload 
```
## ngx-http:
### Agregar configuración basica para un dominio:
```sh
  ngx-http add dominio directorio_raiz
```
#### Ejemplos: 
```sh
  ngx-http add midominio.com      /home/mi_usuario/midominio.com/www/public_html
  ngx-http add www.midominio.com  /home/mi_usuario/midominio.com/www/public_html
  ngx-http add app.midominio.com  /home/mi_usuario/midominio.com/app/public_html
```
EL dominio apuntará al index.html en el directorio raiz indicado.
El archivo de configuración generado se guardará en el directorio /etc/nginx/sites-available.
Puede personalizar la configuración de este archivo si lo requiere.
### Habilitar la configuración de un dominio:
```sh
  ngx-http enable dominio
```
#### Ejemplo: 
```sh
  ngx-http enable app.midominio.com
```
Se creará un enlace simbolico en /etc/nginx/sites-enabled apuntando al archivo de configuración del dominio
### Deshabilitar la configuración de un dominio:
```sh
  ngx-http disable dominio
```
#### Ejemplo: 
```sh
  ngx-http disable app.midominio.com
```
Se eliminará el enlace simbolico en /etc/nginx/sites-enabled que apunta al archivo de configuración del dominio
### Eliminar la configuración de un dominio:
```sh
  ngx-http remove dominio
```
#### Ejemplo: 
```sh
  ngx-http remove app.midominio.com
```
Se eliminará la configuración del directirio /etc/nginx/sites-available.
**Nota:** Es importante que desabilite la configuración antes de eliminarla.
### Redirigir un dominio a otra dirección:
```sh
  ngx-http redirect dominio url
```
#### Ejemplo: 
```sh
  ngx-http redirect app.mindominio.com http://midominio.com/app
```
Se remplazará la configuración del dominio para efectuar la redirección.

## ngx-certificate:
Solicita un certificado SSL para los dominios especificados. Los certificados son firmados por Lets-Encript. Los dominios son verificados y renovados automaticamente.
```sh
  ngx-certificate dominio_1 dominio_2 dominio_n 
```
#### Ejemplo: 
```sh
  ngx-certificate midominio.com www.midominio.com app.mindominio.com
```
Si el certificado ya existia se requerirá elegir si remplazará o conservará el certificado existente.

Al finalizar el proceso se obtiene una salida como la siguiente:
```sh
  - Congratulations! Your certificate and chain have been saved at:
   /etc/letsencrypt/live/midominio.com/fullchain.pem
   Your key file has been saved at:
   /etc/letsencrypt/live/midominio.com/privkey.pem
   Your cert will expire on 2019-09-13.
```
Para este caso el certificado se encontará en: /etc/letsencrypt/live/midominio.com/fullchain.pem

y La llave privada en: etc/letsencrypt/live/midominio.com/privkey.pem

Los cuales podrá usar para configurar acceso seguro mediante https a su sitio web.




