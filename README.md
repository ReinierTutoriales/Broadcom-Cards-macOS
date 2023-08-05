# Broadcom-Cards-macOS
# Bienvenido al repositorio oficial de ReinierTutoriales para Soporte de tarjetas Broadcom en macOS


## Apóyame con una donación 
Mediante [👉PayPal💵](https://www.paypal.com/paypalme/ReinierTutoriales?country.x=US&locale.x=es_XC)


## La protección de integridad del sistema está establecida en 0x803
* Para eso diríjase a NVRAM / Add / 7C436110-AB2A-4BBB-A880-FE41995C9F82.
  * Edite su `csr-active-config`.
  * Agrege el que dejo a continuación en su config.plist.
  * Debería quedar así `csr-active-config | data | 03080000` .


## Deshabilitar AMFI.
 * Agragar en su boot-args `amfi=0x80` .
## Configurar Secure Boot Model
 *  `Secure Boot Model` selecciónalo en `Disabled`
