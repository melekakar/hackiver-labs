# LFI & Log Poisoning – Hackviser Lab

## Amaç
Bu çalışmada kontrollü bir eğitim ortamında
Local File Inclusion (LFI) zafiyetinin
log mekanizmaları ile zincirlenmesi
teorik olarak incelenmiştir.

## İncelenen Kavramlar
- Local File Inclusion (LFI)
- Log Poisoning
- Web Sunucu Logları
- PHP Dosya İşleme Mantığı
- Linux Dosya Sistemi

## Genel Akış
1. Uygulamada dosya yolu alanı analiz edildi
2. Sunucu log dosyalarının okunabildiği tespit edildi
3. Log dosyalarının PHP tarafından işlenmesi durumunda
   oluşabilecek güvenlik riskleri değerlendirildi

## Öğrenilenler
- LFI her zaman RCE’ye dönüşmez
- Dosyanın include edilmesi ile okunması arasında kritik fark vardır
- Log dosyaları güvenli şekilde işlenmezse ciddi risk oluşturur
- Eğitim dokümanları ile gerçek sistem davranışı birebir aynı olmayabilir

## Not
Bu çalışma yalnızca eğitim amaçlıdır.
Herhangi bir gerçek sisteme yönelik saldırı içermez.
