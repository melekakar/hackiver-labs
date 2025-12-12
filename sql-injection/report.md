# SQL Injection Vulnerability Analysis

##  Platform
Hackviser - Web Application Scenario

## Keşif (Reconnaissance)
Uygulamadaki login ve parametre alanları incelendi.
Kullanıcı girdilerinin filtrelenmediği tespit edildi.

##  Zafiyet Türü
SQL Injection (Authentication Bypass / Data Disclosure)

##  Sömürü (Conceptual)
Kullanıcı girdisi doğrudan SQL sorgusuna dahil edilmiştir.
Bu durum, yetkisiz oturum açma ve veri sızıntısına yol açmaktadır.

> Payload detayları **güvenlik ve etik nedenlerle paylaşılmamıştır.**

##  Etki (Impact)
- Yetkisiz kullanıcı girişi
- Hassas verilerin okunması
- Veri bütünlüğünün bozulması

##  Çözüm Önerileri
- Parametreli sorgular (Prepared Statements)
- Input validation
- Least privilege prensibi
- WAF kullanımı

##  Kazanımlar
- SQL Injection tespiti
- Login bypass mantığı
- Güvenli veritabanı erişimi
