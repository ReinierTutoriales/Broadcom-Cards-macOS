# Soporte para Broadcom WiFi y Bluetooth macOS 15 Sequoia
- Bienvenido al repositorio oficial de ReinierTutoriales para Soporte de tarjetas Broadcom en macOS
- Todo el credito del soporte es gracias a la [👉OpenCore Legacy Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher/)

[![](https://img.shields.io/badge/YouTube-informational?style=for-the-badge&logo=telegram&logoColor=white&color=FF0000)](https://youtube.com/c/ReinierTutoriales)
[![](https://img.shields.io/badge/PayPal-informational?style=for-the-badge&logo=paypal&logoColor=white&color=003087)](https://www.paypal.com/paypalme/ReinierTutoriales)
[![](https://img.shields.io/badge/-Telegram-informational?style=for-the-badge&logo=telegram&logoColor=white&color=0088cc)](https://t.me/ReinierTutoriales)
[![](https://img.shields.io/badge/-Twitter-informational?style=for-the-badge&logo=twitter&logoColor=white&color=00aced)](https://twitter.com/ReinierTutorial)
[![](https://img.shields.io/badge/-Facebook-informational?style=for-the-badge&logo=facebook&logoColor=white&color=3b5998)](https://www.facebook.com/ReinierTutoriales)
[![](https://img.shields.io/badge/-Instagram-informational?style=for-the-badge&logo=instagram&logoColor=white&color=C13584)](https://www.instagram.com/reiniertutoriales/)
[![](https://img.shields.io/badge/-Discord-informational?style=for-the-badge&logo=discord&logoColor=white&color=7289da)](https://discord.gg/pQcCDBMn)

</p>

## Dónde Comprar
- [x] Tarjeta PCI Wifi para MacOS: `FENVI T919` [👉💰Compr Aquí💰](https://amzn.to/3OOEQoa)

## 🎥 Video de Ayuda 👇

Haz clic en la imagen para ver el tutorial en YouTube:

[![Video de Ayuda](https://img.youtube.com/vi/ZIEt9QYUu0Y/0.jpg)](https://www.youtube.com/watch?v=ZIEt9QYUu0Y)


## Necesitan inyectar los siguientes kexts
- [x] `IOSkywalk.kext`  [👉Descargar ](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/main/payloads/Kexts/Wifi/IOSkywalkFamily-v1.1.0.zip)
- [x] `IO80211FamilyLegacy.kext`  [👉Descargar ](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/main/payloads/Kexts/Wifi/IO80211FamilyLegacy-v1.0.0.zip)
  * Este Kext tiene un `Complemento` , `AirPortBrcmNIC.kext`asegúrese de que también se inyecte en su `config.plist`
- [x] `AirportBrcmFixup` [👉Descargar ](https://github.com/dortania/build-repo/releases/download/AirportBrcmFixup-c85ca2d/AirportBrcmFixup-2.1.9-RELEASE.zip)
  * Este Kext tiene un `Complemento` , `AirPortBrcmNIC_Injector.kext`asegúrese de que también se inyecte en su  `config.plist`
- [x] `AMFIPass 1.4.1` [👉Descargar ](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/sequoia-development/payloads/Kexts/Acidanthera/AMFIPass-v1.4.1-RELEASE.zip)

- [x] Organice los kexts como se muestra a continuación y agregue MinKernel a su config.plist

 ![Orden de Kexts y MinKernel](IMG/orden-kexts-MinKernel.PNG) 



## Bloquear IOSkywalkFamily 
- [x] `com.apple.iokit.IOSkywalkFamily`  [Referencia](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/e21efa975c0cf228cb36e81a974bc6b4c27c7807/payloads/Config/config.plist#L1695-L1710/)
- [x] Para eso diríjase a `Kernel | Block` y agrege el siguiente parche.
```md
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
