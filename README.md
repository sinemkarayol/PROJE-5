# PROJE-5
README - Tiva C Hibernate Modu Uygulaması

Proje Açıklaması

Bu proje, Tiva C TM4C123GH6PM mikrodenetleyicisini kullanarak Hibernate (Uyku) Modu uygulamasını göstermektedir. Mikrodenetleyici, belirli bir süre (5 saniye) sonra uyanacak şekilde konfigüre edilmiştir. Ayrıca, GPIO durumu korunarak sistem uyandırılabilir.

Kullanılan Bileşenler ve Periferikler
Tiva C TM4C123GH6PM
GPIOF Portu (LED'ler ve butonlar için)
Hibernation (Uyku) Modülü
Gerçek Zamanlı Saat (RTC)

Kütüphaneler
Proje aşağıdaki TivaWare sürücü kütüphanelerini kullanmaktadır:
driverlib/sysctl.h: Sistem saat ayarları ve çevresel birimleri etkinleştirme
driverlib/gpio.h: GPIO pin konfigürasyonu
driverlib/hibernate.h: Hibernate modunun kontrolü
inc/hw_memmap.h, inc/hw_types.h, inc/tm4c123gh6pm.h: Donanım haritası ve tür tanımlamaları

Kod Açıklamaları
Sistem Saati ve Periferik Aktivasyonu
Sistem saatini 50MHz olarak ayarlar.
GPIOF ve Hibernate birimini etkinleştirir.

GPIO Konfigürasyonu
PF1, PF2, PF3 pinleri çıkış olarak tanımlanmıştır (RGB LED kontrolü için).
PF4 pini Pull-up dirençli giriş olarak ayarlanmıştır (Buton kontrolü için).

Hibernate Modülü Konfigürasyonu
HibernateEnableExpClk(SysCtlClockGet()): Hibernate modülünü etkinleştirir.
HibernateGPIORetentionEnable(): Uyandıktan sonra GPIO durumlarını korur.
HibernateRTCSet(0): RTC sayacını sıfırlar.
HibernateRTCEnable(): RTC'yi etkinleştirir.
HibernateRTCMatchSet(0, 5): 5 saniye sonra uyandırma sinyali oluşturur.
HibernateWakeSet(HIBERNATE_WAKE_PIN | HIBERNATE_WAKE_RTC): Uyandırma kaynakları olarak buton ve RTC belirlenir.
HibernateRequest(): Sistemi uyku moduna sokar.

Uyandırma Mekanizması
5 saniye dolduğunda veya PF0 butonuna basıldığında sistem uyanacaktır.
GPIO çıkışları önce LED'i yakar, sonra uyku moduna geçer.

Gelecekteki Geliştirme Olasılıkları
Hafıza (Floating Point) ve PWM Kullanımı
DAC (Digital to Analog Converter) Uygulamaları
DMA (Direct Memory Access) Kullanımı
Derin uyku modları ile güç tüketimini optimize etmek

Derleme ve Çalıştırma
Code Composer Studio (CCS) veya Keil uVision kullanarak projeyi açın.
main.c dosyasını derleyin ve Tiva C kartına yükleyin.
PF1, PF2, PF3 LED'leri yanıp sönecek, ardından sistem uyku moduna geçecektir.
5 saniye sonra veya PF0 butonuna basıldığında sistem uyanacaktır.
