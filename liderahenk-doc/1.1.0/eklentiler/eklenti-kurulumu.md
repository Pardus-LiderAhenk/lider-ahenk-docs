# LiderAhenk Deposundan Eklenti Kurulumu

LiderAhenk eklentileri "**repo.liderahenk.org**" adresinde sunulmaktadır. Pardus bilgisayarlarda bu adres tanımlanarak tüm eklentiler depodan yüklenebilmektedir. Bu deponun sisteminize tanımlanması için uçbirim(konsol)da;

	sudo wget http://repo.liderahenk.org/liderahenk-archive-keyring.asc && sudo apt-key add liderahenk-archive-keyring.asc &&  rm liderahenk-archive-keyring.asc

    
komutları ile "**liderahenk-archive-keyring.asc**" key dosyası indirilerek sisteme yüklenmelidir. Ardından;

	sudo printf  "deb [arch=amd64] http://repo.liderahenk.org/liderahenk stable main" | sudo tee -a

komutu ile depo adresi "**/etc/apt/sources.list**" dosyasına eklenir. 

```
Not: Yukarıdaki adımı uçbirimde bir metin editörü(vi,nano,pico) kullanarak ;

	deb [arch=amd64] http://repo.liderahenk.org/liderahenk stable main

satırını "**/etc/apt/sources.list**" dosyasına elinizle de tanımlayarak yapabilirsiniz. 
```
Daha sonra;

	sudo apt update
    
komutu ile güncel paket listesini alınmalıdır.

Uçbirimde;

	apt search ahenk
    
yazıldığında yüklenebilir eklentiler listelenir.

	sudo apt install ahenk-<paket_adi>
    
komutu ile paket ad(lar)ını belirterek eklentileri yükleyebilirsiniz.