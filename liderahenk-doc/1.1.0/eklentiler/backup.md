# Yedekleme Eklentisi

Dizinlerin yedeklenmesini sağlayan eklentidir. Eklenti, hem görev hem de politika özelliğine sahiptir.

**Politika tarafında,** *"Kullanıcı Adı, Parola, Hedef IP, Hedef Kapı*" ve **"Hedef Dizin"** alanları doldurulur. SSH- anahtarı kullanılacaksa *"SSH Anahtarını Kullan"* seçeneği, LVM Gölgeleme kullanılacaksa *"LVM Gölgeleme Kullan"* seçeneği seçilir.

![backup-plugin](images/backup-plugin.png)

Ekleme butonuna basılmasıyla birlikte yedeklenecek dizinin nasıl yedekleneceği ile ilgili ekran açılır. 

![backup-plugin-ayarlar](images/backup-plugin-ayarlar.png)

Bu ekranda yedeklenmesi istenilen dizinin yolu yazıldığı gibi eğer harici tutulacak dizin varsa bu dizin de **Harici Tutulacaklar** alanında belirtilir.

![backup-plugin-son](images/backup-plugin-son.png)

**Görev tarafı;** Seçilen ahenkle ekranda listelenir. **Yedeklenecek Dizin** bilgisi girilir.

![backup-plugin-gorev](images/yedekleme-ekrani.png)

Daha sonra (daha önce yapılmadı ise) **Yedekleme sunucu ayarları** girilir. Bu ayarlara **Lider** menüsü **Yedekleme Sunucu Konfigurasyonu** ekranından da erişilebilir.

![backup-plugin-sunucu-konf](images/yedekleme-sunucusu-konfiugrasyonu.png)

Bu ayarlar bir defaya mahsus girilir, farklı bir yedekleme sunucusu tanımlanmak istendiğinde bu ayarlar **güncellenmelidir.** Ayarlar sonrası **Çalıştır** butonuna basılır.

![backup-plugin-sonuc](images/yedekleme-sonuc.png)

Yedekleme verinin büyüklüğüne göre uzun sürebilir. **Lider**  menüsü **Yedekleme Görevleri Ekranı**ndan takip edilebilir.

Alınan yedeğin **%** 'lik durumu boyutu, süresi vb bilgiler ekranda  gösterilmektedir. Bu veriler **yedeklenecek ağın durmuna ve verinin büyüklüğüne** göre değişkenlik göstermektedir.
