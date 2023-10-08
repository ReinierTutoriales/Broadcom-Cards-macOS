# Soporte Broadcom para macOS
- Bienvenido al repositorio oficial de ReinierTutoriales para Soporte de tarjetas Broadcom en macOS
- Todo el credito del soporte es gracias a la [👉OpenCore Legacy Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher/)

## Dónde Comprar
- [x] Tarjeta PCI Wifi para MacOS: `FENVI T919` [👉💰Compr Aquí💰](https://amzn.to/3OOEQoa)

## Video de Ayuda👇
[![Alt text](https://img.youtube.com/vi/ZIEt9QYUu0Y/0.jpg)](https://www.youtube.com/watch?v=ZIEt9QYUu0Y)

## Necesitan inyectar los siguientes kexts
- [x] `IOSkywalk.kext`  [👉Descargar ](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/e21efa975c0cf228cb36e81a974bc6b4c27c7807/payloads/Kexts/Wifi/IOSkywalkFamily-v1.0.0.zip/)
- [x] `IO80211FamilyLegacy.kext`  [👉Descargar ](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/e21efa975c0cf228cb36e81a974bc6b4c27c7807/payloads/Kexts/Wifi/IO80211FamilyLegacy-v1.0.0.zip/)
  * Este Kext tiene un `Child | Hijo` , `AirPortBrcmNIC.kext`asegúrese de que también se inyecte en su `config.plist`
  * Configúrelo en todos ellos el `MinKernel` para `23.0.0`. Con esto garatizaria que los parches y kexts solo se apliquen en Sonoma, evitando conflitos con otras versiones de macOS que no lo necesitan.

## El siguiente kexts debes bloquearlo 
- [x] `com.apple.iokit.IOSkywalkFamily`  [Referencia](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/e21efa975c0cf228cb36e81a974bc6b4c27c7807/payloads/Config/config.plist#L1695-L1710/)
- [x] Para eso diríjase a `Kernel | Block` y agrege el siguiente parche.
```md
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<array>
	<dict>
		<key>Arch</key>
		<string>Any</string>
		<key>Comment</key>
		<string>Allow IOSkywalk Downgrade</string>
		<key>Enabled</key>
		<false/>
		<key>Identifier</key>
		<string>com.apple.iokit.IOSkywalkFamily</string>
		<key>MaxKernel</key>
		<string></string>
		<key>MinKernel</key>
		<string>23.0.0</string>
		<key>Strategy</key>
		<string>Exclude</string>
	</dict>
</array>
</plist>

```

## La protección de integridad del sistema está establecida en 0x803
- [x] Para eso diríjase a `NVRAM | Add | 7C436110-AB2A-4BBB-A880-FE41995C9F82`
  * Edite su `csr-active-config`
  * Cambie `00000000` por `03080000`


## Deshabilitar AMFI
- [x] Agragar en su boot-args `amfi=0x80`
- [x] Si no decea utilizar `amfi=0x80` pudes agregar [AMFIPass.kext](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/main/payloads/Kexts/Acidanthera/AMFIPass-v1.3.1-RELEASE.zip) y el boot-arg `-amfipassbeta` 
## Configurar Secure Boot Model
- [x]  `Secure Boot Model` selecciónalo en `Disabled`.
  * Restablezca NVRAM o agregue `csr-active-config` Tipo `string`  a `NVRAM` - `Delete` - `7C436110-AB2A-4BBB-A880-FE41995C9F82` para asegurarse de que la nueva variable esté configurada.



## Para finalizar Finalmente
- [x] Necesitan reiniciar el sistema.
- [x] Despues de este reinicio  necesitan ejecutar `OpenCore Legacy Patcher` [👉 1.0.1 ](https://github.com/dortania/OpenCore-Legacy-Patcher/releases)

> [!IMPORTANT]
> The only official source for this kext is the Actions tab of the `ChefKissInc/NootedRed` GitHub repository, provided entirely free of charge.
