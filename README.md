# 🔒 Localhost HTTPS Certificates

Self-signed HTTPS certificates for **localhost**  
Validity: **until year 5000** (for development use only).

---

## 📂 Directory Structure

Each folder contains 2 files:
- `cert.crt` → Certificate
- `cert.key` → Private Key

Available algorithms:
- RSA 2048
- RSA 4096
- ECDSA P-384
- ECDSA P-521
- ED25519
- ED448

---

## ⚠️ Security Notes
- **For localhost / development only.**
- **Not for production or public domains.**
- Keep `.key` private and secure.

---

## 🛠️ Usage Examples

### 1. Nginx
```nginx
server {
    listen 443 ssl;
    server_name localhost;

    ssl_certificate     /path/to/RSA\ 4096/cert.crt;
    ssl_certificate_key /path/to/RSA\ 4096/cert.key;

    location / {
        root   html;
        index  index.html;
    }
}
```
Reload Nginx:
```bash
nginx -s reload
```

### 2. Apache (httpd)
```apache
<VirtualHost _default_:443>
    ServerName localhost

    SSLEngine on
    SSLCertificateFile "/path/to/RSA 4096/cert.crt"
    SSLCertificateKeyFile "/path/to/RSA 4096/cert.key"

    DocumentRoot "/var/www/html"
</VirtualHost>
```
Restart Apache:
```bash
systemctl restart apache2
```

### 3. Node.js (Express)
```js
import fs from 'fs';
import https from 'https';
import express from 'express';

const app = express();

const options = {
  key: fs.readFileSync('./RSA 4096/cert.key'),
  cert: fs.readFileSync('./RSA 4096/cert.crt')
};

https.createServer(options, app).listen(443, () => {
  console.log('Server running at https://localhost');
});
```

### 4. Docker (Nginx container)
Structure:
```
docker-nginx/
├─ certs/
│   ├─ cert.crt
│   └─ cert.key
├─ nginx.conf
└─ html/
   └─ index.html
```
Run container:
```bash
docker run -d -p 443:443   -v ./certs:/etc/nginx/certs   -v ./nginx.conf:/etc/nginx/nginx.conf:ro   -v ./html:/usr/share/nginx/html   nginx
```

---

## ✅ Trusting the certificate

- **Windows**: Import `.crt` into **Trusted Root Certification Authorities**  
- **Linux**:  
```bash
sudo cp cert.crt /usr/local/share/ca-certificates/localhost.crt
sudo update-ca-certificates
```
- **macOS**: Import `.crt` into **Keychain Access → Always Trust**

---

## ⚡ Algorithm Comparison

| Algorithm   | Key length | Signing speed | Verify speed | Security | Notes |
|-------------|------------|---------------|--------------|----------|-------|
| RSA 2048    | 2048 bit   | Medium        | Medium       | Secure   | Widely supported |
| RSA 4096    | 4096 bit   | Slow          | Very slow    | Very strong | Heavy, rare in dev |
| ECDSA P-384 | ~192-bit sec | Fast        | Very fast    | Very strong | Best balance |
| ECDSA P-521 | ~256-bit sec | Fast        | Very fast    | Extremely strong | For advanced test |
| ED25519     | 256 bit    | Very fast     | Very fast    | Very strong | Modern, light, not always supported |
| ED448       | 456 bit    | Fast          | Fast         | Extremely strong | Rare, research use |

---

## 🎯 Recommended Choice

- General dev use → **RSA 2048** or **ECDSA P-384**  
- Stronger security → **RSA 4096**  
- Best balance perf + security → **ECDSA P-384**  
- Crypto research → **ED25519 / ED448**

---

# 🔒 Chứng chỉ HTTPS cho Localhost (Tiếng Việt)

Chứng chỉ HTTPS **tự ký** cho `localhost`  
Thời hạn sử dụng: **đến năm 5000** (chỉ dùng trong môi trường phát triển).

---

## 📂 Cấu trúc thư mục

Mỗi thư mục gồm 2 tệp:
- `cert.crt` → Chứng chỉ
- `cert.key` → Khóa bí mật

Thuật toán có sẵn:
- RSA 2048
- RSA 4096
- ECDSA P-384
- ECDSA P-521
- ED25519
- ED448

---

## ⚠️ Lưu ý bảo mật
- **Chỉ dùng trong localhost / phát triển.**
- **Không dùng cho production/public.**
- Khóa `.key` cần bảo mật.

---

## 🛠️ Hướng dẫn sử dụng

### 1. Nginx
```nginx
server {
    listen 443 ssl;
    server_name localhost;

    ssl_certificate     /path/to/RSA\ 4096/cert.crt;
    ssl_certificate_key /path/to/RSA\ 4096/cert.key;

    location / {
        root   html;
        index  index.html;
    }
}
```
Reload:
```bash
nginx -s reload
```

### 2. Apache
```apache
<VirtualHost _default_:443>
    ServerName localhost

    SSLEngine on
    SSLCertificateFile "/path/to/RSA 4096/cert.crt"
    SSLCertificateKeyFile "/path/to/RSA 4096/cert.key"

    DocumentRoot "/var/www/html"
</VirtualHost>
```
Restart:
```bash
systemctl restart apache2
```

### 3. Node.js (Express)
```js
import fs from 'fs';
import https from 'https';
import express from 'express';

const app = express();

const options = {
  key: fs.readFileSync('./RSA 4096/cert.key'),
  cert: fs.readFileSync('./RSA 4096/cert.crt')
};

https.createServer(options, app).listen(443, () => {
  console.log('Server chạy tại https://localhost');
});
```

### 4. Docker (Nginx container)
Cấu trúc:
```
docker-nginx/
├─ certs/
│   ├─ cert.crt
│   └─ cert.key
├─ nginx.conf
└─ html/
   └─ index.html
```
Chạy container:
```bash
docker run -d -p 443:443   -v ./certs:/etc/nginx/certs   -v ./nginx.conf:/etc/nginx/nginx.conf:ro   -v ./html:/usr/share/nginx/html   nginx
```

---

## ✅ Cách tin cậy chứng chỉ

- **Windows**: Import `.crt` vào **Trusted Root Certification Authorities**  
- **Linux**:  
```bash
sudo cp cert.crt /usr/local/share/ca-certificates/localhost.crt
sudo update-ca-certificates
```
- **macOS**: Import `.crt` vào **Keychain Access → Always Trust**

---

## ⚡ So sánh thuật toán

| Thuật toán   | Độ dài khóa | Tốc độ ký | Tốc độ xác minh | Mức bảo mật | Ghi chú |
|--------------|------------|-----------|-----------------|-------------|---------|
| RSA 2048     | 2048 bit   | Trung bình | Trung bình | An toàn | Phổ biến nhất |
| RSA 4096     | 4096 bit   | Chậm | Rất chậm | Cực mạnh | Ít dùng trong dev |
| ECDSA P-384  | ~192 bit bảo mật | Nhanh | Rất nhanh | Rất mạnh | Khuyến nghị dùng |
| ECDSA P-521  | ~256 bit bảo mật | Nhanh | Rất nhanh | Cực mạnh | Dùng để test nâng cao |
| ED25519      | 256 bit    | Rất nhanh | Rất nhanh | Rất mạnh | Mới, nhẹ, chưa hỗ trợ rộng |
| ED448        | 456 bit    | Nhanh | Nhanh | Cực mạnh | Ít hỗ trợ |

---

## 🎯 Khuyến nghị lựa chọn

- Dev chung → **RSA 2048** hoặc **ECDSA P-384**  
- Muốn mạnh hơn → **RSA 4096**  
- Hiệu năng tốt + bảo mật cao → **ECDSA P-384**  
- Nghiên cứu crypto → **ED25519 / ED448**
