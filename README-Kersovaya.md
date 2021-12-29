# devops-netology
**Sarkisyan Aleksey**

**Выполнение Курсовой работы**


**Задание 1**

Конфигурация файла виртуальной машины 

```
Vagrant.configure("2") do |config|
	config.vm.box = "bento/ubuntu-20.04"
	config.vm.provider :virtualbox do |vb|
		vb.memory = "3024"
		vb.cpus="3"
	end
end
```


**Задание 2.**

## Установка ufw

```
sudo apt update
sudo apt install nginx

sudo ufw allow 22
sudo ufw allow 443

sudo ufw enable
```

**Задание 3.**

```
vagrant@vagrant:~$ curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
OK
vagrant@vagrant:~$ sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
Hit:1 http://archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]
Get:3 http://archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Get:4 https://apt.releases.hashicorp.com focal InRelease [9,495 B]
Get:5 http://archive.ubuntu.com/ubuntu focal-backports InRelease [108 kB]
Get:6 https://apt.releases.hashicorp.com focal/main amd64 Packages [41.1 kB]
Get:7 http://archive.ubuntu.com/ubuntu focal-updates/main i386 Packages [574 kB]
Get:8 http://security.ubuntu.com/ubuntu focal-security/main amd64 Packages [1,069 kB]
Get:9 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [1,400 kB]
Get:10 http://archive.ubuntu.com/ubuntu focal-updates/main Translation-en [283 kB]
Get:11 http://archive.ubuntu.com/ubuntu focal-updates/restricted amd64 Packages [616 kB]
Get:12 http://archive.ubuntu.com/ubuntu focal-updates/restricted Translation-en [88.1 kB]
Get:13 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [884 kB]
Get:14 http://archive.ubuntu.com/ubuntu focal-updates/universe i386 Packages [654 kB]
Get:15 http://archive.ubuntu.com/ubuntu focal-updates/universe Translation-en [193 kB]
Get:16 http://archive.ubuntu.com/ubuntu focal-backports/main amd64 Packages [42.0 kB]
Get:17 http://archive.ubuntu.com/ubuntu focal-backports/main i386 Packages [34.5 kB]
Get:18 http://archive.ubuntu.com/ubuntu focal-backports/main Translation-en [10.0 kB]
Get:19 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 Packages [18.9 kB]
Get:20 http://archive.ubuntu.com/ubuntu focal-backports/universe i386 Packages [10.5 kB]
Get:21 http://archive.ubuntu.com/ubuntu focal-backports/universe Translation-en [7,492 B]
Get:22 http://security.ubuntu.com/ubuntu focal-security/main i386 Packages [345 kB]
Get:23 http://security.ubuntu.com/ubuntu focal-security/main Translation-en [197 kB]
Get:24 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 Packages [566 kB]
Get:25 http://security.ubuntu.com/ubuntu focal-security/restricted Translation-en [80.9 kB]
Get:26 http://security.ubuntu.com/ubuntu focal-security/universe i386 Packages [525 kB]
Get:27 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [668 kB]
Get:28 http://security.ubuntu.com/ubuntu focal-security/universe Translation-en [112 kB]
Fetched 8,764 kB in 2s (4,014 kB/s)
Reading package lists... Done
vagrant@vagrant:~$ sudo apt-get update && sudo apt-get install vault
Hit:1 http://archive.ubuntu.com/ubuntu focal InRelease
Hit:2 http://archive.ubuntu.com/ubuntu focal-updates InRelease
Hit:3 https://apt.releases.hashicorp.com focal InRelease
Hit:4 http://security.ubuntu.com/ubuntu focal-security InRelease
Hit:5 http://archive.ubuntu.com/ubuntu focal-backports InRelease
Reading package lists... Done
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following NEW packages will be installed:
  vault
0 upgraded, 1 newly installed, 0 to remove and 106 not upgraded.
Need to get 69.4 MB of archives.
After this operation, 188 MB of additional disk space will be used.
Get:1 https://apt.releases.hashicorp.com focal/main amd64 vault amd64 1.9.2 [69.4 MB]
Fetched 69.4 MB in 7s (10.2 MB/s)
Selecting previously unselected package vault.
(Reading database ... 48552 files and directories currently installed.)
Preparing to unpack .../archives/vault_1.9.2_amd64.deb ...
Unpacking vault (1.9.2) ...
Setting up vault (1.9.2) ...
Generating Vault TLS key and self-signed certificate...
Generating a RSA private key
...................................................++++
.................++++
writing new private key to 'tls.key'
-----
Vault TLS key and self-signed certificate have been generated in '/opt/vault/tls'.
vagrant@vagrant:~$ vauly
-bash: vauly: command not found
vagrant@vagrant:~$ vault
Usage: vault <command> [args]

Common commands:
    read        Read data and retrieves secrets
    write       Write data, configuration, and secrets
    delete      Delete secrets and configuration
    list        List data or secrets
    login       Authenticate locally
    agent       Start a Vault agent
    server      Start a Vault server
    status      Print seal and HA status
    unwrap      Unwrap a wrapped secret

Other commands:
    audit          Interact with audit devices
    auth           Interact with auth methods
    debug          Runs the debug command
    kv             Interact with Vault's Key-Value storage
    lease          Interact with leases
    monitor        Stream log messages from a Vault server
    namespace      Interact with namespaces
    operator       Perform operator-specific tasks
    path-help      Retrieve API help for paths
    plugin         Interact with Vault plugins and catalog
    policy         Interact with policies
    print          Prints runtime configurations
    secrets        Interact with secrets engines
    ssh            Initiate an SSH session
    token          Interact with tokens
```



**Задание 4.**


```
vagrant@vagrant:~$ vault secrets enable pki
Success! Enabled the pki secrets engine at: pki/
vagrant@vagrant:~$ vault secrets tune -max-lease-ttl=87600h pki
Success! Tuned the secrets engine at: pki/
vagrant@vagrant:~$ vault write -field=certificate pki/root/generate/internal \
>      common_name="example.com" \
>      ttl=87600h > CA_cert.crt
vagrant@vagrant:~$ vault write pki/config/urls \
>      issuing_certificates="$VAULT_ADDR/v1/pki/ca" \
>      crl_distribution_points="$VAULT_ADDR/v1/pki/crl"
Success! Data written to: pki/config/urls
vagrant@vagrant:~$ vault secrets enable -path=pki_int pki
Success! Enabled the pki secrets engine at: pki_int/
vagrant@vagrant:~$ vault secrets tune -max-lease-ttl=43800h pki_int
]Success! Tuned the secrets engine at: pki_int/
vagrant@vagrant:~$ vault write -format=json pki_int/intermediate/generate/intern                                        al \
>      common_name="example.com Intermediate Authority" \
>      | jq -r '.data.csr' > pki_intermediate.csr
vagrant@vagrant:~$ vault write -format=json pki/root/sign-intermediate csr=@pki_                                        intermediate.csr \
>      format=pem_bundle ttl="43800h" \
>      | jq -r '.data.certificate' > intermediate.cert.pem
vagrant@vagrant:~$ vault write pki_int/intermediate/set-signed certificate=@inte                                        rmediate.cert.pem
Success! Data written to: pki_int/intermediate/set-signed
vagrant@vagrant:~$ vault write pki_int/roles/example-dot-com \
>      allowed_domains="example.com" \
>      allow_subdomains=true \
>      max_ttl="720h"
Success! Data written to: pki_int/roles/example-dot-com
vagrant@vagrant:~$ vault write pki_int/issue/example-dot-com common_name="test.e                                        xample.com" ttl="720h"
Key                 Value
---                 ------

ca_chain            [-----BEGIN CERTIFICATE-----
MIIDpjCCAo6gAwIBAgIUXIV9Cw5Z9Yoql6Jj6k9PGWhDhJMwDQYJKoZIhvcNAQEL
BQAwFjEUMBIGA1UEAxMLZXhhbXBsZS5jb20wHhcNMjExMjI5MTM1NTEzWhcNMjYx
MjI4MTM1NTQzWjAtMSswKQYDVQQDEyJleGFtcGxlLmNvbSBJbnRlcm1lZGlhdGUg
QXV0aG9yaXR5MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAv9/Fvn6B
4Q+SsVT/Ag7cjUFhwbHDVjIHktbQbqemAZ1jyedKGxl7i8PVLSy/Wvb8lcxpsP41
7vQ3PycmTUZ6INEemP7OeGlraW89Pmc9DFNaV+sp5WswTOkIFeUvjbN5apOAfP08
GDN9RXNjojntZdlVawxBz7Re6aGegFkP1r4R0JyzdZpn1Yzt07emjHkzq6f3Rjg8
Welo94dFAH0ZC9iaShIjuB2tD1S1PAgFZre/NYZ47U0PGg8pcJvMCKEOwd+nD9FX
fvlgTRTipH8K2WRwRosrI34Q0Xu55R0VJ+K9yKA35juJFElop1UZVANTwZXthM5n
fTzGep7tdzM4WwIDAQABo4HUMIHRMA4GA1UdDwEB/wQEAwIBBjAPBgNVHRMBAf8E
BTADAQH/MB0GA1UdDgQWBBTj5OFjijR2ojlRCUeMev4SGVxT8jAfBgNVHSMEGDAW
gBSY2SNsR/HB0zrk1p+wThPl44wpATA7BggrBgEFBQcBAQQvMC0wKwYIKwYBBQUH
MAKGH2h0dHA6Ly8xMjcuMC4wLjE6ODIwMC92MS9wa2kvY2EwMQYDVR0fBCowKDAm
oCSgIoYgaHR0cDovLzEyNy4wLjAuMTo4MjAwL3YxL3BraS9jcmwwDQYJKoZIhvcN
AQELBQADggEBAH7Evju2/zEztPZ6/qAV+27QurLFu7YHi1qrxVVu9sg17eQWzMdD
SWR8ir5A035TUEa5fTh+H/sJIj018ug4aESBb8sbz3nig4aCP8H4qaP+pR7JXitQ
blUOKywUPSy2BBYFqAKoDhOL0ULHsdlK1I+ZtJDIy2+DidUp/0LAaLKgynFkVpik
wMJReo3W4tPYdV9SmciYEl9HUH08nJHOuMVFx9xnNh4EXDfsdaCHkZ+MDAiuaCyC
55cqnW15KHBvWeCgG1WXwr6D6aFAHWxjNWB4KwwKn042oNCOQUDE6oIQI2C528Mv
qx/CoO4/TIFkxIkLzBmzaN6QX6egfOMs4XY=
-----END CERTIFICATE-----]
certificate         -----BEGIN CERTIFICATE-----
MIIDZjCCAk6gAwIBAgIUN3cOMcDF/waS9R0lRnqVnFltsoowDQYJKoZIhvcNAQEL
BQAwLTErMCkGA1UEAxMiZXhhbXBsZS5jb20gSW50ZXJtZWRpYXRlIEF1dGhvcml0
eTAeFw0yMTEyMjkxMzU1NDBaFw0yMjAxMjgxMzU2MDlaMBsxGTAXBgNVBAMTEHRl
c3QuZXhhbXBsZS5jb20wggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDH
OOR8ymeqrShmMyb9C8z/TNAkZBU3LBg0iFeZ4D0Q8oqzZoUyTybhfPSBXUhjMkA8
fIBqNEUlYPnChp/JyOWHeNOWVQFbvZnK0DZAJB7ZkFPI7MDoreqrvDz6jwiV5+IE
fzuLzUrXcxaRVGXosaZ8ZyPYFnV6SoLubGXRVeELEY6e62bOHymxIvx6uFO5uX1y
8owZWq9YtwvbofROp4XQuRzGkAh/GHdAcVoD7u3YEcpHSlXil/4o0BNe0AV2bHRx
qAPe8Os5Ry+tCrDBHzSBEpMkqfcJ/EbkhEolf8fC5KWnv+qUoLGWUIpLrk54lBEU
Lh9oXKhnl5qgN/HHQM7/AgMBAAGjgY8wgYwwDgYDVR0PAQH/BAQDAgOoMB0GA1Ud
JQQWMBQGCCsGAQUFBwMBBggrBgEFBQcDAjAdBgNVHQ4EFgQUE3Emb69KaM7KvvWz
sHPytvj8tYcwHwYDVR0jBBgwFoAU4+ThY4o0dqI5UQlHjHr+EhlcU/IwGwYDVR0R
BBQwEoIQdGVzdC5leGFtcGxlLmNvbTANBgkqhkiG9w0BAQsFAAOCAQEAET9Ka0Re
4rBfWfu4mr8/iuejncmjTqewrO9ZJ5yT/IutCL0/Psc78EEjnVARh42gv3jPQMw7
oUSqycFdfGFp1axAvQbJlj/I4ahcGx/23wM15G6Z4p7Y/UZDx/QQR3xF+AXlPoZL
2bYucbrgbkZESvB4sdQ8amY5mrCiqclDGCQkQFpAi/fwVlk5XXbC8x9vMhB/OTSm
4WM/Hzj293nXxyyvznBihNOCkKo/Th02cq+/V+m5qtNWPK5IsSBzRhvrZfTyY0sn
RTEi/FCFFEp7xAnNyGWpcGcMa1Mnpiq+uPgFs6FZqfN626OTSiiBETjFQO7RCRLE
PLuZ/54LAD8S9w==
-----END CERTIFICATE-----
expiration          1643378169
issuing_ca          -----BEGIN CERTIFICATE-----
MIIDpjCCAo6gAwIBAgIUXIV9Cw5Z9Yoql6Jj6k9PGWhDhJMwDQYJKoZIhvcNAQEL
BQAwFjEUMBIGA1UEAxMLZXhhbXBsZS5jb20wHhcNMjExMjI5MTM1NTEzWhcNMjYx
MjI4MTM1NTQzWjAtMSswKQYDVQQDEyJleGFtcGxlLmNvbSBJbnRlcm1lZGlhdGUg
QXV0aG9yaXR5MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAv9/Fvn6B
4Q+SsVT/Ag7cjUFhwbHDVjIHktbQbqemAZ1jyedKGxl7i8PVLSy/Wvb8lcxpsP41
7vQ3PycmTUZ6INEemP7OeGlraW89Pmc9DFNaV+sp5WswTOkIFeUvjbN5apOAfP08
GDN9RXNjojntZdlVawxBz7Re6aGegFkP1r4R0JyzdZpn1Yzt07emjHkzq6f3Rjg8
Welo94dFAH0ZC9iaShIjuB2tD1S1PAgFZre/NYZ47U0PGg8pcJvMCKEOwd+nD9FX
fvlgTRTipH8K2WRwRosrI34Q0Xu55R0VJ+K9yKA35juJFElop1UZVANTwZXthM5n
fTzGep7tdzM4WwIDAQABo4HUMIHRMA4GA1UdDwEB/wQEAwIBBjAPBgNVHRMBAf8E
BTADAQH/MB0GA1UdDgQWBBTj5OFjijR2ojlRCUeMev4SGVxT8jAfBgNVHSMEGDAW
gBSY2SNsR/HB0zrk1p+wThPl44wpATA7BggrBgEFBQcBAQQvMC0wKwYIKwYBBQUH
MAKGH2h0dHA6Ly8xMjcuMC4wLjE6ODIwMC92MS9wa2kvY2EwMQYDVR0fBCowKDAm
oCSgIoYgaHR0cDovLzEyNy4wLjAuMTo4MjAwL3YxL3BraS9jcmwwDQYJKoZIhvcN
AQELBQADggEBAH7Evju2/zEztPZ6/qAV+27QurLFu7YHi1qrxVVu9sg17eQWzMdD
SWR8ir5A035TUEa5fTh+H/sJIj018ug4aESBb8sbz3nig4aCP8H4qaP+pR7JXitQ
blUOKywUPSy2BBYFqAKoDhOL0ULHsdlK1I+ZtJDIy2+DidUp/0LAaLKgynFkVpik
wMJReo3W4tPYdV9SmciYEl9HUH08nJHOuMVFx9xnNh4EXDfsdaCHkZ+MDAiuaCyC
55cqnW15KHBvWeCgG1WXwr6D6aFAHWxjNWB4KwwKn042oNCOQUDE6oIQI2C528Mv
qx/CoO4/TIFkxIkLzBmzaN6QX6egfOMs4XY=
-----END CERTIFICATE-----
private_key         -----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAxzjkfMpnqq0oZjMm/QvM/0zQJGQVNywYNIhXmeA9EPKKs2aF
Mk8m4Xz0gV1IYzJAPHyAajRFJWD5woafycjlh3jTllUBW72ZytA2QCQe2ZBTyOzA
6K3qq7w8+o8IlefiBH87i81K13MWkVRl6LGmfGcj2BZ1ekqC7mxl0VXhCxGOnutm
zh8psSL8erhTubl9cvKMGVqvWLcL26H0TqeF0LkcxpAIfxh3QHFaA+7t2BHKR0pV
4pf+KNATXtAFdmx0cagD3vDrOUcvrQqwwR80gRKTJKn3CfxG5IRKJX/HwuSlp7/q
lKCxllCKS65OeJQRFC4faFyoZ5eaoDfxx0DO/wIDAQABAoIBAA3WXchtJpYsQMoY
c3TQBQUWiL5+VRrn7SZ48dy2PoeW0Rt023uLE+BFlZYGrKh3LQ8GdsTprIPUIITq
ZN7XHVozgj7G2LlOiggUPjBmUd46sBccmqmOquYSxQmCNc5ztLcrPy+OqswcKk0d
15Y6AJ5Ta6HurWo5Eq8MyGWp2V+zUQc0+cuHfWkoeUeAGiEV+TFm1RCPHrNiWHt7
jEJxExW7riAciClMUDFTS056HUbUt9dx98peeZIQHmZknnxIRQtjjgdizyPxwMym
nfkHd0OxYO7KZVLHzNMW/z/OsRHZ6DbBRE4Ors+cJpuJ+ZZegkL8BMP7J9fZEVsz
9uOo1oECgYEA0aQtbVnvl8rsWnbOoV1qeLH/mB9XdE5agcpUPRPeQymI2A96Wykx
a9iXV4J+Iz3rvlIZF0gppxw3Ast09KvewaMpzxzZjgG9WVG9tY7PJfWDI7JXH+0j
NJxWQoN6iZMC2Go4odpr8+FqUMiXO9rt5fpLdzMFWbgOea4pI9r+8HkCgYEA80bj
tfBKD9aV4I31TYNx+8plUSSE2NGdG/YVCpORnECtk6+8lEM0WHkzu1HlG4h9Z4F2
kvFckmhI9FCZVDozpDQjsasZPySXhI/5JmhyO88CzXf8Oc1gETg3y9yf9p7XyZqT
taTkYgVEW0Xei59xfkA5gRDnEG3MGQ6Nj9stDTcCgYBgfHKX+KOoNjIP9MxnQkpl
oG7lwc8LbaCESe35anKKcMxVvNHwsQXZAAevtBR//djJcJmxuHnLOtYqyB9dGNle
P81XUIzkqfJO8Ksiq8a1Tsj7nfIxdIAWj7m3xTGZrfrKRiEohRHYXjADXD8Wwk1p
4ofnJalZwLeQ01KF+R4K6QKBgAnnXOXPPnSem8NkhBP/wegqOS2weugIwIie4ARq
NYdS6r4UbWzrv3nKlVyO3PDeAZzxHE6nHMmpDS9FCLjxFaEdrkZRXNnBN5nh8pap
sdzVdJvAwrfnsH2C+GKIPMrhdI90h4bhi5qh9EJy+bhdaVVmb/DdK0rz7VcnzIOK
vK7JAoGBAJUpwCXUZs3WXLVFfsnO1NE7bpvLP3MCMv/Pc5W/82/4bWeHJ18iaOkN
jw17mHnxXU3oitSb00Z8lxnB6Iszn3mfcu96ifxtQxhTVxPRsgWc3XPTbr5IsRhn
fBRf6r+GDsH5EKMzn8P8BIpkM2xcsvh0cBInUvo3YHQUP/NKlh3d
-----END RSA PRIVATE KEY-----
private_key_type    rsa
serial_number       37:77:0e:31:c0:c5:ff:06:92:f5:1d:25:46:7a:95:9c:59:6d:b2:8a
```

**Задание 5.**

Установл корневой сертификат.

**Задание 6**

```
vagrant@vagrant:~$ sudo apt install nginx
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  fontconfig-config fonts-dejavu-core libfontconfig1 libgd3 libjbig0
  libjpeg-turbo8 libjpeg8 libnginx-mod-http-image-filter
  libnginx-mod-http-xslt-filter libnginx-mod-mail libnginx-mod-stream libtiff5
  libwebp6 libx11-6 libx11-data libxcb1 libxpm4 nginx-common nginx-core
Suggested packages:
  libgd-tools fcgiwrap nginx-doc ssl-cert
The following NEW packages will be installed:
  fontconfig-config fonts-dejavu-core libfontconfig1 libgd3 libjbig0
  libjpeg-turbo8 libjpeg8 libnginx-mod-http-image-filter
  libnginx-mod-http-xslt-filter libnginx-mod-mail libnginx-mod-stream libtiff5
  libwebp6 libx11-6 libx11-data libxcb1 libxpm4 nginx nginx-common nginx-core
0 upgraded, 20 newly installed, 0 to remove and 107 not upgraded.
Need to get 3,165 kB of archives.
After this operation, 11.1 MB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://archive.ubuntu.com/ubuntu focal/main amd64 libxcb1 amd64 1.14-2 [44                                             .7 kB]
Get:2 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libx11-data all                                              2:1.6.9-2ubuntu1.2 [113 kB]
Get:3 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libx11-6 amd64 2                                             :1.6.9-2ubuntu1.2 [575 kB]
Get:4 http://archive.ubuntu.com/ubuntu focal/main amd64 fonts-dejavu-core all 2.                                             37-1 [1,041 kB]
Get:5 http://archive.ubuntu.com/ubuntu focal/main amd64 fontconfig-config all 2.                                             13.1-2ubuntu3 [28.8 kB]
Get:6 http://archive.ubuntu.com/ubuntu focal/main amd64 libfontconfig1 amd64 2.1                                             3.1-2ubuntu3 [114 kB]
Get:7 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libjpeg-turbo8 a                                             md64 2.0.3-0ubuntu1.20.04.1 [117 kB]
Get:8 http://archive.ubuntu.com/ubuntu focal/main amd64 libjpeg8 amd64 8c-2ubunt                                             u8 [2,194 B]
Get:9 http://archive.ubuntu.com/ubuntu focal/main amd64 libjbig0 amd64 2.1-3.1bu                                             ild1 [26.7 kB]
Get:10 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libwebp6 amd64                                              0.6.1-2ubuntu0.20.04.1 [185 kB]
Get:11 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libtiff5 amd64                                              4.1.0+git191117-2ubuntu0.20.04.2 [162 kB]
Get:12 http://archive.ubuntu.com/ubuntu focal/main amd64 libxpm4 amd64 1:3.5.12-                                             1 [34.0 kB]
Get:13 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libgd3 amd64 2.                                             2.5-5.2ubuntu2.1 [118 kB]
Get:14 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 nginx-common al                                             l 1.18.0-0ubuntu1.2 [37.5 kB]
Get:15 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libnginx-mod-ht                                             tp-image-filter amd64 1.18.0-0ubuntu1.2 [14.4 kB]
Get:16 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libnginx-mod-ht                                             tp-xslt-filter amd64 1.18.0-0ubuntu1.2 [12.7 kB]
Get:17 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libnginx-mod-ma                                             il amd64 1.18.0-0ubuntu1.2 [42.5 kB]
Get:18 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libnginx-mod-st                                             ream amd64 1.18.0-0ubuntu1.2 [67.3 kB]
Get:19 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 nginx-core amd6                                             4 1.18.0-0ubuntu1.2 [425 kB]
Get:20 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 nginx all 1.18.                                             0-0ubuntu1.2 [3,620 B]
Fetched 3,165 kB in 2s (1,442 kB/s)
Preconfiguring packages ...
Selecting previously unselected package libxcb1:amd64.
(Reading database ... 41575 files and directories currently installed.)
Preparing to unpack .../00-libxcb1_1.14-2_amd64.deb ...
Unpacking libxcb1:amd64 (1.14-2) ...
Selecting previously unselected package libx11-data.
Preparing to unpack .../01-libx11-data_2%3a1.6.9-2ubuntu1.2_all.deb ...
Unpacking libx11-data (2:1.6.9-2ubuntu1.2) ...
Selecting previously unselected package libx11-6:amd64.
Preparing to unpack .../02-libx11-6_2%3a1.6.9-2ubuntu1.2_amd64.deb ...
Unpacking libx11-6:amd64 (2:1.6.9-2ubuntu1.2) ...
Selecting previously unselected package fonts-dejavu-core.
Preparing to unpack .../03-fonts-dejavu-core_2.37-1_all.deb ...
Unpacking fonts-dejavu-core (2.37-1) ...
Selecting previously unselected package fontconfig-config.
Preparing to unpack .../04-fontconfig-config_2.13.1-2ubuntu3_all.deb ...
Unpacking fontconfig-config (2.13.1-2ubuntu3) ...
Selecting previously unselected package libfontconfig1:amd64.
Preparing to unpack .../05-libfontconfig1_2.13.1-2ubuntu3_amd64.deb ...
Unpacking libfontconfig1:amd64 (2.13.1-2ubuntu3) ...
Selecting previously unselected package libjpeg-turbo8:amd64.
Preparing to unpack .../06-libjpeg-turbo8_2.0.3-0ubuntu1.20.04.1_amd64.deb ...
Unpacking libjpeg-turbo8:amd64 (2.0.3-0ubuntu1.20.04.1) ...
Selecting previously unselected package libjpeg8:amd64.
Preparing to unpack .../07-libjpeg8_8c-2ubuntu8_amd64.deb ...
Unpacking libjpeg8:amd64 (8c-2ubuntu8) ...
Selecting previously unselected package libjbig0:amd64.
Preparing to unpack .../08-libjbig0_2.1-3.1build1_amd64.deb ...
Unpacking libjbig0:amd64 (2.1-3.1build1) ...
Selecting previously unselected package libwebp6:amd64.
Preparing to unpack .../09-libwebp6_0.6.1-2ubuntu0.20.04.1_amd64.deb ...
Unpacking libwebp6:amd64 (0.6.1-2ubuntu0.20.04.1) ...
Selecting previously unselected package libtiff5:amd64.
Preparing to unpack .../10-libtiff5_4.1.0+git191117-2ubuntu0.20.04.2_amd64.deb .                                             ..
Unpacking libtiff5:amd64 (4.1.0+git191117-2ubuntu0.20.04.2) ...
Selecting previously unselected package libxpm4:amd64.
Preparing to unpack .../11-libxpm4_1%3a3.5.12-1_amd64.deb ...
Unpacking libxpm4:amd64 (1:3.5.12-1) ...
Selecting previously unselected package libgd3:amd64.
Preparing to unpack .../12-libgd3_2.2.5-5.2ubuntu2.1_amd64.deb ...
Unpacking libgd3:amd64 (2.2.5-5.2ubuntu2.1) ...
Selecting previously unselected package nginx-common.
Preparing to unpack .../13-nginx-common_1.18.0-0ubuntu1.2_all.deb ...
Unpacking nginx-common (1.18.0-0ubuntu1.2) ...
Selecting previously unselected package libnginx-mod-http-image-filter.
Preparing to unpack .../14-libnginx-mod-http-image-filter_1.18.0-0ubuntu1.2_amd6                                             4.deb ...
Unpacking libnginx-mod-http-image-filter (1.18.0-0ubuntu1.2) ...
Selecting previously unselected package libnginx-mod-http-xslt-filter.
Preparing to unpack .../15-libnginx-mod-http-xslt-filter_1.18.0-0ubuntu1.2_amd64                                             .deb ...
Unpacking libnginx-mod-http-xslt-filter (1.18.0-0ubuntu1.2) ...
Selecting previously unselected package libnginx-mod-mail.
Preparing to unpack .../16-libnginx-mod-mail_1.18.0-0ubuntu1.2_amd64.deb ...
Unpacking libnginx-mod-mail (1.18.0-0ubuntu1.2) ...
Selecting previously unselected package libnginx-mod-stream.
Preparing to unpack .../17-libnginx-mod-stream_1.18.0-0ubuntu1.2_amd64.deb ...
Unpacking libnginx-mod-stream (1.18.0-0ubuntu1.2) ...
Selecting previously unselected package nginx-core.
Preparing to unpack .../18-nginx-core_1.18.0-0ubuntu1.2_amd64.deb ...
Unpacking nginx-core (1.18.0-0ubuntu1.2) ...
Selecting previously unselected package nginx.
Preparing to unpack .../19-nginx_1.18.0-0ubuntu1.2_all.deb ...
Unpacking nginx (1.18.0-0ubuntu1.2) ...
Setting up libxcb1:amd64 (1.14-2) ...
Setting up nginx-common (1.18.0-0ubuntu1.2) ...
Created symlink /etc/systemd/system/multi-user.target.wants/nginx.service → /lib                                             /systemd/system/nginx.service.
Setting up libjbig0:amd64 (2.1-3.1build1) ...
Setting up libnginx-mod-http-xslt-filter (1.18.0-0ubuntu1.2) ...
Setting up libx11-data (2:1.6.9-2ubuntu1.2) ...
Setting up libwebp6:amd64 (0.6.1-2ubuntu0.20.04.1) ...
Setting up fonts-dejavu-core (2.37-1) ...
Setting up libjpeg-turbo8:amd64 (2.0.3-0ubuntu1.20.04.1) ...
Setting up libx11-6:amd64 (2:1.6.9-2ubuntu1.2) ...
Setting up libjpeg8:amd64 (8c-2ubuntu8) ...
Setting up libnginx-mod-mail (1.18.0-0ubuntu1.2) ...
Setting up libxpm4:amd64 (1:3.5.12-1) ...
Setting up fontconfig-config (2.13.1-2ubuntu3) ...
Setting up libnginx-mod-stream (1.18.0-0ubuntu1.2) ...
Setting up libtiff5:amd64 (4.1.0+git191117-2ubuntu0.20.04.2) ...
Setting up libfontconfig1:amd64 (2.13.1-2ubuntu3) ...
Setting up libgd3:amd64 (2.2.5-5.2ubuntu2.1) ...
Setting up libnginx-mod-http-image-filter (1.18.0-0ubuntu1.2) ...
Setting up nginx-core (1.18.0-0ubuntu1.2) ...
Setting up nginx (1.18.0-0ubuntu1.2) ...
Processing triggers for ufw (0.36-6ubuntu1) ...
Processing triggers for systemd (245.4-4ubuntu3.11) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.2) ...
vagrant@vagrant:~$ sudo ufw app list
Available applications:
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
  OpenSSH
vagrant@vagrant:~$ systemctl status nginx
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset:>
     Active: active (running) since Tue 2021-12-28 13:49:19 UTC; 44s ago
       Docs: man:nginx(8)
   Main PID: 2046 (nginx)
      Tasks: 4 (limit: 3427)
     Memory: 5.9M
     CGroup: /system.slice/nginx.service
             ├─2046 nginx: master process /usr/sbin/nginx -g daemon on; master_>
             ├─2047 nginx: worker process
             ├─2048 nginx: worker process
             └─2049 nginx: worker process
```
   
   
**Задание 7**

Создаю каталог для будущего сайта

```
vagrant@vagrant:~$ mkdir -p /var/www/example.com/html
mkdir: cannot create directory ‘/var/www/example.com’: Permission denied
vagrant@vagrant:~$ sudo mkdir -p /var/www/example.com/html
vagrant@vagrant:~$ sudo chown -R $USER:$USER /var/www/
```
Создаю файл конфигурации для сайта

```
vagrant@vagrant:/etc/nginx$ sudo vi /sites-available/example.com.conf

server {
    listen 80;
    listen [::]:80;

    server_name test.example.com;
    return 301 https://test.example.com$request_uri;
}


server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;

    server_name test.example.com;
    root /var/www/example.com/html;
    index index.html index.xml;

    ssl_certificate cert.crt;
    ssl_certificate_key private.key;
    
}

vagrant@vagrant:/etc/nginx$ sudo ln -s /etc/nginx/sites-available/example.com.conf /etc/nginx/sites-enabled/
vagrant@vagrant:/etc/nginx$ sudo nginx -t
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful 
vagrant@vagrant:/etc/nginx$ sudo systemctl restart nginx
```


**Задание 8**

![Задание 8](/kursovaya/8.PNG)


**Задание 9**

Скрипт
```
#!/usr/bin/env bash

export VAULT_ADDR=http://127.0.0.1:8200
export VAULT_TOKEN=root
vault write -format=json pki_int/issue/example-dot-com common_name="test.example.com" ttl="120h" > /home/vagrant/ce1.crt
cat /home/vagrant/ce1.crt | jq -r .data.certificate > /home/vagrant/certif.crt
cat /home/vagrant/ce1.crt | jq -r .data.ca_chain[0] > /home/vagrant/chain.crt
cat /home/vagrant/ce1.crt | jq -r .data.private_key > /home/vagrant/private.key
cat /home/vagrant/certif.crt /home/vagrant/chain.crt > /home/vagrant/cert.crt
sudo mv -f /home/vagrant/cert.crt /etc/nginx/
sudo mv -f /home/vagrant/private.key /etc/nginx/
sudo systemctl restart nginx
```
Файлы сертификатов cert.crt и private.key после выполнения скрипта изменяются, это виджно по времени измениния ниже и тут же смотрю статус nginx
```
vagrant@vagrant:/etc/nginx$ ls -l
total 76
-rw-rw-r-- 1 vagrant vagrant 2567 Dec 29 16:47 cert.crt
drwxr-xr-x 2 root    root    4096 May 25  2021 conf.d
-rw-r--r-- 1 root    root    1077 Feb  4  2019 fastcgi.conf
-rw-r--r-- 1 root    root    1007 Feb  4  2019 fastcgi_params
-rw-r--r-- 1 root    root    2837 Feb  4  2019 koi-utf
-rw-r--r-- 1 root    root    2223 Feb  4  2019 koi-win
-rw-r--r-- 1 root    root    3957 Feb  4  2019 mime.types
drwxr-xr-x 2 root    root    4096 May 25  2021 modules-available
drwxr-xr-x 2 root    root    4096 Dec 28 13:49 modules-enabled
-rw-r--r-- 1 root    root    1490 Feb  4  2019 nginx.conf
-rw-rw-r-- 1 vagrant vagrant 1679 Dec 29 16:47 private.key
-rw-r--r-- 1 root    root     180 Feb  4  2019 proxy_params
-rw-r--r-- 1 root    root     636 Feb  4  2019 scgi_params
drwxr-xr-x 2 root    root    4096 Dec 29 14:51 sites-available
drwxr-xr-x 2 root    root    4096 Dec 28 17:42 sites-enabled
drwxr-xr-x 2 root    root    4096 Dec 28 13:49 snippets
-rw-r--r-- 1 root    root     664 Feb  4  2019 uwsgi_params
-rw-r--r-- 1 root    root    3071 Feb  4  2019 win-utf
vagrant@vagrant:/etc/nginx$ sudo vi /sites-available/example.com.conf
vagrant@vagrant:/etc/nginx$ sudo vi /sites-available/example.com.conf
vagrant@vagrant:/etc/nginx$ cd sites-available/
vagrant@vagrant:/etc/nginx/sites-available$ ls -l
total 8
-rw-r--r-- 1 root root 2416 Mar 26  2020 default
-rw-r--r-- 1 root root  839 Dec 29 14:51 example.com.conf
vagrant@vagrant:/etc/nginx/sites-available$ sudo vi example.com.conf
vagrant@vagrant:/etc/nginx/sites-available$ cd
vagrant@vagrant:~$ ./script.sh
vagrant@vagrant:~$ cd /etc/nginx/
vagrant@vagrant:/etc/nginx$ ls -l
total 76
-rw-rw-r-- 1 vagrant vagrant 2567 Dec 29 14:44 cert1.crt
-rw-rw-r-- 1 vagrant vagrant 2567 Dec 29 16:50 cert.crt
drwxr-xr-x 2 root    root    4096 May 25  2021 conf.d
-rw-r--r-- 1 root    root    1077 Feb  4  2019 fastcgi.conf
-rw-r--r-- 1 root    root    1007 Feb  4  2019 fastcgi_params
-rw-r--r-- 1 root    root    2837 Feb  4  2019 koi-utf
-rw-r--r-- 1 root    root    2223 Feb  4  2019 koi-win
-rw-r--r-- 1 root    root    3957 Feb  4  2019 mime.types
drwxr-xr-x 2 root    root    4096 May 25  2021 modules-available
drwxr-xr-x 2 root    root    4096 Dec 28 13:49 modules-enabled
-rw-r--r-- 1 root    root    1490 Feb  4  2019 nginx.conf
-rw-rw-r-- 1 vagrant vagrant 1679 Dec 29 16:50 private.key
-rw-r--r-- 1 root    root     180 Feb  4  2019 proxy_params
-rw-r--r-- 1 root    root     636 Feb  4  2019 scgi_params
drwxr-xr-x 2 root    root    4096 Dec 29 16:50 sites-available
drwxr-xr-x 2 root    root    4096 Dec 28 17:42 sites-enabled
drwxr-xr-x 2 root    root    4096 Dec 28 13:49 snippets
-rw-r--r-- 1 root    root     664 Feb  4  2019 uwsgi_params
-rw-r--r-- 1 root    root    3071 Feb  4  2019 win-utf
vagrant@vagrant:/etc/nginx$ sudo systemctl status nginx
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2021-12-29 16:50:24 UTC; 3min 58s ago
       Docs: man:nginx(8)
    Process: 1842 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
    Process: 1847 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
   Main PID: 1857 (nginx)
      Tasks: 4 (limit: 3427)
     Memory: 4.4M
     CGroup: /system.slice/nginx.service
             ├─1857 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
             ├─1858 nginx: worker process
             ├─1859 nginx: worker process
             └─1860 nginx: worker process

Dec 29 16:50:24 vagrant systemd[1]: Starting A high performance web server and a reverse proxy server...
Dec 29 16:50:24 vagrant systemd[1]: Started A high performance web server and a reverse proxy server.
```

**Задание 10**

Задание crontab

41 19 29 * 3 /home/vagrant/script.sh > /tmp/script.log 2>&1

Надеюсь достаточно понятно тут показал, что отпечаток, то есть сертификат сменился на следующую минуту после запуска кроном скрипта.

![Задание 9](/kursovaya/9_1.PNG)

![Задание 9](/kursovaya/9_2.PNG)




