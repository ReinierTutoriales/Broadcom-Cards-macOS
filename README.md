# 🚨 Soporte para Broadcom WiFi y Bluetooth en macOS 15 Sequoia

Bienvenido al repositorio oficial de **ReinierTutoriales** para el soporte de tarjetas **Broadcom** en **macOS 15 Sequoia**.

Todo el crédito del soporte es gracias a la increíble labor de [👉 **OpenCore Legacy Patcher**](https://github.com/dortania/OpenCore-Legacy-Patcher/).

---

## 📱 Conéctate con nosotros

Visita nuestras plataformas para más información y soporte:

[![Foro - ReinierTutoriales](https://img.shields.io/badge/Foro-181818?style=for-the-badge&logo=forum&logoColor=white)](https://www.reiniertutoriales.com/)
[![YouTube](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://youtube.com/c/ReinierTutoriales)
[![PayPal](https://img.shields.io/badge/PayPal-0070ba?style=for-the-badge&logo=paypal&logoColor=white)](https://www.paypal.com/paypalme/ReinierTutoriales)

---

## 📱 Redes Sociales y Comunidad

[![Telegram](https://img.shields.io/badge/Telegram-0088cc?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/ReinierTutoriales)
[![Twitter](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/ReinierTutorial)
[![Facebook](https://img.shields.io/badge/Facebook-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://www.facebook.com/ReinierTutoriales)
[![Instagram](https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://www.instagram.com/reiniertutoriales/)
[![Discord](https://img.shields.io/badge/Discord-7289da?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/pQcCDBMn)

---

## ☕ Apóyanos

[![Buy Me a Coffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-ffdd00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black)](https://www.buymeacoffee.com/reiniertutoriales)
[![Patreon](https://img.shields.io/badge/Patreon-F96854?style=for-the-badge&logo=patreon&logoColor=white)](https://www.patreon.com/ReinierTutoriales)

</p>


## 🛒 Dónde Comprar

- ✅ **Tarjeta PCI Wifi para macOS:** _FENVI T919_  
  [👉💰 Comprar Aquí 💰](https://amzn.to/3OOEQoa)

## 🎥 Video de Ayuda 👇

Haz clic en la imagen para ver el tutorial en YouTube:

[![Video de Ayuda](https://img.youtube.com/vi/ZIEt9QYUu0Y/0.jpg)](https://www.youtube.com/watch?v=ZIEt9QYUu0Y)


## 💻 Necesitan inyectar los siguientes kexts

1. ✅ **`IOSkywalk.kext`**  
   [👉 Descargar](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/main/payloads/Kexts/Wifi/IOSkywalkFamily-v1.1.0.zip)

2. ✅ **`IO80211FamilyLegacy.kext`**  
   [👉 Descargar](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/main/payloads/Kexts/Wifi/IO80211FamilyLegacy-v1.0.0.zip)  
   *Este Kext tiene un complemento, `AirPortBrcmNIC.kext`. Asegúrese de que también se inyecte en su `config.plist`.*

3. ✅ **`AirportBrcmFixup`**  
   [👉 Descargar](https://github.com/dortania/build-repo/releases/download/AirportBrcmFixup-c85ca2d/AirportBrcmFixup-2.1.9-RELEASE.zip)  
   *Este Kext tiene un complemento, `AirPortBrcmNIC_Injector.kext`. Asegúrese de que también se inyecte en su `config.plist`.*

4. ✅ **`AMFIPass 1.4.1`**  
   [👉 Descargar](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/sequoia-development/payloads/Kexts/Acidanthera/AMFIPass-v1.4.1-RELEASE.zip)

5. ✅ **Organización de los kexts**  
   Organice los kexts como se muestra a continuación y agregue `MinKernel` a su `config.plist`.

---

**Nota:** Asegúrese de que todos los complementos mencionados también estén correctamente inyectados en su `config.plist`.

## Orden de Kexts y MinKernel

![Imagen que muestra el orden de Kexts y MinKernel en el archivo config.plist](IMG/orden-kexts-MinKernel.PNG)



## 🚫 **Bloquear IOSkywalkFamily**

1. ✅ **`com.apple.iokit.IOSkywalkFamily`**  
   [Referencia](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/e21efa975c0cf228cb36e81a974bc6b4c27c7807/payloads/Config/config.plist#L1695-L1710/)

2. ✅ **Pasos para bloquear:**
   Dirígete a `Kernel | Block` y agrega el siguiente parche en tu `config.plist`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
   <plist version="1.0">
   <dict>
      <key>0</key>
      <dict>
         <key>Arch</key>
         <string>Any</string>
         <key>Comment</key>
         <string>Allow IOSkywalk Downgrade</string>
         <key>Enabled</key>
         <true/>
         <key>Identifier</key>
         <string>com.apple.iokit.IOSkywalkFamily</string>
         <key>MaxKernel</key>
         <string></string>
         <key>MinKernel</key>
         <string>23.0.0</string>
         <key>Strategy</key>
         <string>Exclude</string>
      </dict>
   </dict>
   </plist>


```
## Configurar Secure Boot Model
- [x]  `Secure Boot Model` selecciónalo en `Disabled`.

## La protección de integridad del sistema está establecida en 0x803
- [x] Para eso diríjase a `NVRAM | Add | 7C436110-AB2A-4BBB-A880-FE41995C9F82`
  * Edite su `csr-active-config`
  * Cambie `00000000` por `03080000`
- [x] Agragar en su boot-args Opcionales
  * En caso de que no se pueden aplicar parches raíz  `amfi=0x80`
  * Resuelve el bloqueo de electrones con SIP abierto a partir de macOS 12.3 `ipc_control_port_options=0`

## Para no tener que reiniciar la NVRAM
- [x] Para eso diríjase a `NVRAM | Delete | 7C436110-AB2A-4BBB-A880-FE41995C9F82`
  * Agregar dos valores `csr-active-config` y `boot-args` de tipo String, como se muestra en la imagen a continuación
 
 ![Valores](IMG/Valores%20NVRAM-Delete-9F82.PNG) 

## Para finalizar Finalmente
- [x] Necesitan reiniciar el sistema.
- [x] Despues de este reinicio  necesitan ejecutar `OpenCore Legacy Patcher` [👉 Repositorio ](https://github.com/dortania/OpenCore-Legacy-Patcher/releases)



> **⚠️ [IMPORTANTE]**
>
> Todo esto es gracias a los proyectos que han desarrollado la solución, como **[Dortania](https://dortania.github.io/OpenCore-Legacy-Patcher/INSTALLER.html)** y **[OpenCore Legacy Patcher](https://dortania.github.io/OpenCore-Legacy-Patcher/INSTALLER.html)**.
>
> Estos proyectos permiten tener compatibilidad con **Wireless Broadcom WiFi** y **Bluetooth** en **macOS 14 Sonoma** y **macOS 15 Sequoia**.
