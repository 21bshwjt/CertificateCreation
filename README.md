# CertificateCreation

```powershell
[Version]
Signature="$Windows NT$"
[NewRequest]
Subject = "CN=bshwjtfn.bshwjt.com" ; For a wildcard use "CN=*.CONTOSO.COM" for example
; For an empty subject use the following line instead or remove the Subject line entierely
; Subject =
Exportable = TRUE ; Private key is not exportable
KeyLength = 2048 ; Common key sizes: 512, 1024, 2048, 4096, 8192, 16384
KeySpec = 1 ; AT_KEYEXCHANGE
KeyUsage = 0xA0 ; Digital Signature, Key Encipherment
MachineKeySet = True ; The key belongs to the local computer account
ProviderName = "Microsoft RSA SChannel Cryptographic Provider"
ProviderType = 12
SMIME = FALSE
RequestType = CMC
[Extensions]
2.5.29.17 = "{text}"
_continue_ = "DNS=bshwjtfn.bshwjt.com&"
_continue_ = "iPAddress=20.49.104.56"
```
