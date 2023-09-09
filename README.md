# Soporte Broadcom para macOS
# Bienvenido al repositorio oficial de ReinierTutoriales para Soporte de tarjetas Broadcom en macOS
# Todo el credito del soporte es gracias a la [👉Guía de Dortania](https://github.com/dortania/OpenCore-Legacy-Patcher/)

## Dónde Comprar
- [x] Tarjeta PCI Wifi para MacOS: `FENVI T919` [👉💰Compr Aquí💰](https://amzn.to/3OOEQoa)

## Necesitan inyectar los siguientes kexts
- [x] `IOSkywalk.kext`  [👉Descargar ](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/e21efa975c0cf228cb36e81a974bc6b4c27c7807/payloads/Kexts/Wifi/IOSkywalkFamily-v1.0.0.zip/)
- [x] `IO80211FamilyLegacy.kext`  [👉Descargar ](https://github.com/dortania/OpenCore-Legacy-Patcher/blob/e21efa975c0cf228cb36e81a974bc6b4c27c7807/payloads/Kexts/Wifi/IO80211FamilyLegacy-v1.0.0.zip/)

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
- [x] Para eso diríjase a `NVRAM | Add | 7C436110-AB2A-4BBB-A880-FE41995C9F82`.
  * Edite su `csr-active-config`
  * Cambie `00000000` por `03080000`


## Deshabilitar AMFI
- [x] Agragar en su boot-args `amfi=0x80`
## Configurar Secure Boot Model
- [x]  `Secure Boot Model` selecciónalo en `Disabled`
      * Restablezca NVRAM o agregue `csr-active-config` Tipo `string`  a `NVRAM` - `Delete` - `7C436110-AB2A-4BBB-A880-FE41995C9F82` para asegurarse de que la nueva variable esté configurada.



## Para finalizar Finalmente
- [x] Necesitan reiniciar el sistema.
- [x] Despues de este reinicio  necesitan ejecutar `OpenCore Legacy Patcher` [👉 0.6.9 Nightly ](https://github.com/dortania/OpenCore-Legacy-Patcher/pull/1077/)
