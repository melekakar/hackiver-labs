# File Upload to Remote Code Execution (RCE)

## 📌 Platform
Hackviser - InnovifyAI Scenario

## 🔍 Keşif (Reconnaissance)
Uygulamada dosya yükleme fonksiyonu incelendi.
Yüklenen dosyaların uzantı ve içerik kontrolü yapılmadığı tespit edildi.

## ⚠️ Zafiyet Türü
Unrestricted File Upload  
→ Remote Code Execution (RCE)

## 🧪 Sömürü (Conceptual)
Yüklenen dosya sunucu tarafından çalıştırılabilir dizine kaydedildi.
Bu durum, sunucu üzerinde komut çalıştırılmasına yol açmaktadır.

> Payload detayları **güvenlik nedeniyle paylaşılmamıştır.**

## 🎯 Etki (Impact)
- Sunucu üzerinde yetkisiz komut çalıştırma
- Hassas dosyalara erişim
- Tam sistem ele geçirilmesi riski

## 🛡️ Çözüm Önerileri
- Dosya uzantısı ve MIME type doğrulaması
- Upload dizininin çalıştırılabilir olmaması
- Web application firewall (WAF) kullanımı
- Least privilege prensibi

## 🧠 Kazanımlar
- File upload zafiyetleri
- Web shell mantığı
- Linux kullanıcı yetkileri
