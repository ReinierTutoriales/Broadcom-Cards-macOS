# Soporte Broadcom para macOS
# Bienvenido al repositorio oficial de ReinierTutoriales para Soporte de tarjetas Broadcom en macOS
# Todo el credito del soporte es gracias a la [👉Guía de Dortania](https://github.com/dortania/OpenCore-Legacy-Patcher/)

## Dónde Comprar
* Tarjeta PCI Wifi para MacOS: `FENVI T919` [👉Compr Aquí💵](https://amzn.to/3OOEQoa)


## La protección de integridad del sistema está establecida en 0x803
* Para eso diríjase a `NVRAM` - `Add` - `7C436110-AB2A-4BBB-A880-FE41995C9F82`.
  * Edite su `csr-active-config`.
  * Cambie `00000000` por `03080000`.


## Deshabilitar AMFI.
 * Agragar en su boot-args `amfi=0x80` .
## Configurar Secure Boot Model
 *  `Secure Boot Model` selecciónalo en `Disabled`


## El siguiente kexts debes bloquearlo 
 * `com.apple.iokit.IOSkywalkFamily`  [Referencia](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/e21efa975c0cf228cb36e81a974bc6b4c27c7807/payloads/Config/config.plist#L1695-L1710/)
 * Para eso diríjase a `Kernel` - `Block` y agrege el siguiente parche.
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

## Necesitan inyectar los siguientes kexts
 * `IOSkywalk.kext`  [👉Descargar ](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/e21efa975c0cf228cb36e81a974bc6b4c27c7807/payloads/Kexts/Wifi/IOSkywalkFamily-v1.0.0.zip/)
 * `IO80211FamilyLegacy.kext`  [👉Descargar ](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/e21efa975c0cf228cb36e81a974bc6b4c27c7807/payloads/Kexts/Wifi/IO80211FamilyLegacy-v1.0.0.zip/)

## Para finalizar Finalmente.
 * Necesitan reiniciar el sistema.
* Despues de este reinicio  necesitan ejecutar `OpenCore Legacy Patcher` [👉 0.6.9 Nightly ](https://github.com/dortania/OpenCore-Legacy-Patcher/pull/1077/)
