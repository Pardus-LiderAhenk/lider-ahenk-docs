# Kaynak Yönetimi Eklentisi

Eklenti bir görev eklentisidir. Ahenk makinelerindeki kaynakların anlık kullanımına dair kullanıcıya bilgi vermekte ve aynı zamanda bu kaynakların yönetimini sağlamaktadır. Eklenti iki görevden oluşmaktadır. Bu görevler aşağıda belirtilmektedir.

## Kaynak Kullanım Bilgisi

Bir Ahenk için çalıştırılan bu görev, Ahenk makinesinin anlık kaynak kullanım bilgisini kullanıcıya sunmaktadır.

![Kaynak Kullanımı](images/kaynak-kullanimi.png)

## Kaynak Kullanım Alarmları

* Bir Ahenk makine için çalıştırılan bu görev için kullanıcı tarafından bir zaman aralığı belirlenir.(Örneğin 50 saniyede bir ölçüm yapılsın)
* Bellek alarmı için kısıtlamalar belirlenir (Örneğin bellek kullanımı yüzde 70’i geçtiğinde- alarm verilsin)
* Bellek   kullanımı   esnasında   belirtilen   kullanım   kısıtını   belirli   bir   sürede   kaç   kere- aşıldığında yeni bir uyarı verileceği bilgileri belirlenir.(Örneğin; bir önceki maddede belirtilen kısıtlar doğrultusunda oluşturulan bellek alarmı sayısı 6 dakika içerisinde 3 kere yinelenirse alarm verilsin)
* İşlemci   alarmı   için   kısıtlamalar   belirlenir   (Örneğin   işlemci   kullanımı   yüzde   70’i- geçtiğinde alarm verilsin)
* İşlemci   kullanımı   esnasında   belirtilen   kullanım   kısıtını   belirli   bir   sürede   kaç   kere- aşıldığında yeni bir uyarı verileceği bilgileri belirlenir.(Örneğin; bir önceki maddede belirtilen kısıtlar doğrultusunda oluşturulan işlemci alarmı sayısı 6 dakika içerisinde 3 kere yinelenirse alarm verilsin)
* Alarmların türleri belirlenir (mail gönder, makineyi kapat).
* Alarmın hangi mail adresine bildirileceği bilgisi belirlenir.

**"Değişken Ortalama"** butonuna tıklanıldığında ölçümler belirtilen kısıtlar dahilinde başlar. Tablo ve Bellek-İşlemci kullanım şablonları dinamik olarak güncellenir. Bellek kullanım şablonu her bir ölçüm sonucunda ortalama bellek kullanım miktarını, İşlemci kullanım şablonu ise ortalama işlemci kullanımını göstermektedir. 

![Kaynak Kullanımı](images/kaynak-kullanım-veri-listesi.png)

Ölçümler, kullanıcı **"Sabit Ortalama"** butonuna tıklayana kadar devam edecektir.

![Kaynak Kullanımı](images/kaynak-kullanım-veri-listesi-duzenle.png)

 Bu esnada oluşturulan her bir alarm **"Alarm Listesi"** sekmesinden görülebilmektedir.

![Kaynak Kullanımı](images/kaynak-kullanım-veri-listesi-alarm.png)