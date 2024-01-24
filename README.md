# Manual Certificate Creation - Active Directory Certificate Service

### 'request.inf' includes the necessary configurations for the certificate request
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
### There exists a certificate template named 'azurecert,' and it is configured to have the capability of exporting the private key
<img width="450" src="https://github.com/21bshwjt/CertificateCreation/blob/main/screenshots/tmpl.png?raw=true">

##### Above Template was cloned from the '**Web Server**' Template.
                     
```powershell
certreq -new request.inf request.req
certreq -attrib "CertificateTemplate:azurecert" -submit request.req request.cer
```

### Sample multiple SAN - Not tested 
```powershell
[Version]

Signature="$Windows NT$"

[NewRequest]
Subject = "CN=name.contoso.com,O=CSR Demo,OU=IT,L=Brussels,S=Brussels,E=certificates@contoso.com,C=BE"

;EncipherOnly = FALSE
Exportable = TRUE   ; TRUE = Private key is exportable
KeyLength = 2048     ; Valid key sizes: 1024, 2048, 4096, 8192, 16384
KeySpec = 1          ; Key Exchange – Required for encryption
KeyUsage = 0xA0      ; Digital Signature, Key Encipherment
MachineKeySet = True
ProviderName = "Microsoft RSA SChannel Cryptographic Provider"

RequestType = PKCS10 ; or CMC.

[EnhancedKeyUsageExtension]
OID=1.3.6.1.5.5.7.3.1 ; Server Authentication
;OID=1.3.6.1.5.5.7.3.2 ; Client Authentication  // Uncomment if you need a mutual TLS authentication

[Extensions]
2.5.29.17 = "{text}"
_continue_ = "dns=name.contoso.com&"
_continue_ = "dns=othername.contoso.com"
```
