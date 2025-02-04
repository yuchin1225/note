## 憑證 pfx 轉換 cert / key

### 1. 產生 伺服器憑證檔 ( server.cer )
```bash
Windows

openssl pkcs12 -in server.pfx -nokeys -password "pass:vEryComPleXPw" -out - 2>nul | openssl x509 -out server.crt

Linux Shell 環境

openssl pkcs12 -in server.pfx -nokeys -password "pass:vEryComPleXPw" -out - 2>/dev/null | openssl x509 -out server.crt
```

### 2. 產生 私密金鑰檔 ( server.key )

```bash
openssl pkcs12 -in server.pfx -nocerts -password "pass:vEryComPleXPw" -nodes -out server.key
```
