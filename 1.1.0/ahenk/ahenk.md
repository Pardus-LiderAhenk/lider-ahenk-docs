# Ahenk Kayıt

Ahenk paketi "repo.liderahenk.org" adresinde sunulmaktadır. Pardus bilgisayarlarda bu adres tanımlanarak ahenk paketi depodan yüklenebilmektedir. Bu deponun sisteminize tanımlanması için uçbirim(konsol)da;

	sudo wget http://repo.liderahenk.org/liderahenk-archive-keyring.asc && sudo apt-key add liderahenk-archive-keyring.asc &&  rm liderahenk-archive-keyring.asc

komutları ile "liderahenk-archive-keyring.asc" key dosyası indirilerek sisteme yüklenmelidir. Ardından;

	sudo printf  "deb [arch=amd64] http://repo.liderahenk.org/liderahenk stable main" | sudo tee -a /etc/apt/sources.list

komutu ile depo adresi "/etc/apt/sources.list" dosyasına eklenir. 

```
Not: Yukarıdaki adımı uçbirimde bir metin editörü(vi,nano,pico) yardımı ile ;

	deb [arch=amd64] http://repo.liderahenk.org/liderahenk stable main

satırını "/etc/apt/sources.list" dosyasına elinizle de tanımlayabilirsiniz.
``` 

Daha sonra;

	sudo apt update

komutu ile güncel paket listesini alınmalıdır.

	sudo apt install ahenk

komutu ile güncel ahenk paketi kurulumu yapıldıktan sonra yapılandırma dosyasından;

    host = 
    receiverjid = 
    receiverresource = 
    servicename =

alanları girilerek yapılandırma dosyası kaydedilerek çıkılır. Örneğin ahenk yapılandırma dosyası;

	sudo nano /etc/ahenk/ahenk.conf

ile açılarak şu şekilde düzenlenirse;

    [BASE]
    logconfigurationfilepath = /etc/ahenk/log.conf
    dbpath = /etc/ahenk/ahenk.db

    [PLUGIN]
    pluginfolderpath = /usr/share/ahenk/plugins/
    mainmodulename = main

    [CONNECTION]
    uid = 
    password = 
    host =  192.168.56.1
    port = 5222
    use_tls = false
    receiverjid = lider_sunucu
    receiverresource = Smack
    servicename = im.liderahenk.org
    receivefileparam = /tmp/

    [SESSION]
    agreement_timeout = 30
    registration_timeout = 30
    get_policy_timeout = 30

    [MACHINE]
    type = default
    agreement = 1 
    
Düzenleme işlemi tamamlandıktan sonra;

	sudo systemctl restart ahenk.service

komutu ahenk servisi tekrar başlatılarak, ahenk'in kayıt olması sağlanır.

## LiderAhenk Deposundan Eklenti Kurulumu

Uçbirimde;

	apt search ahenk-
    
yazıldığında yüklenebilir eklentiler listelenir. Örnek sorgulama sonucu;

```
Sıralama... Bitti
Tam Metin Arama... Bitti
ahenk/stable 1.0.0-7.1 all [şundan yükseltilebilir: 1.0.0-7]
  The client side of the Lider Ahenk Project

ahenk-antivirus/stable 1.1 amd64
  Lider Ahenk ahenk-antivirus plugin

ahenk-backup/stable 1.1 amd64
  Lider Ahenk backup plugin

ahenk-browser/stable,now 1.1 amd64 [kurulu,otomatik-kaldırılabilir]
  Lider Ahenk browser plugin
```
şeklinde paketler listelenir.

	sudo apt install ahenk-<paket_adi>

komutu ile paket ad(lar)ını birer boşluk ile yazarak eklentileri yükleyebilirsiniz.
Örneğin:
	
    sudo apt install ahenk-resource-usage ahenk-manage-root
    
şeklinde **Kaynak Kullanım** ve **Root Parolası Yönetimi** paketlerini yazarak kurulum yapabilirsiniz.
    
Ahenk kurulumunda;
* Betik
* Uygulama(Paket) Yönetimi
* Servis Yönetimi 
* Uzak Masaüstü 
* Ulak
* Ağ Yönetimi 
* Kaynak Kullanımı 
* Oturum Yönetimi 
* Root Parolası Yönetimi 
* Yerel Kullanıcı 
* OpenLDAP İstemci Ayarları
* Usb 
* Kullanıcı Ayrıcalıkları 
* Sudoers 
* Örün Tarayıcı 

eklentileri kurulu olarak gelir. Diğer paketleri yukarıda anlatılan şekilde kurabilirsiniz.