#LiderArayüz Kurulumu

LiderArayüz bileşeni **LiderAhenk Github** ** sayfasında ve  "**repo.liderahenk.org**" adresinde sunulmaktadır. İki farklı şeklilde kurulum yapılabilir.

##İndir-Kur

Github [sayfasından](https://github.com/Pardus-LiderAhenk/lider-console/releases/download/v1.1/lider-console_1.1_all.deb)  **.deb** uzantılı paket indirilerek uçbirimde ;

	sudo dpkg -i lider-console_1.1_all.deb
    
komutu ile yükleme yapılır. Daha sonra **Uygulamalar Menüsü > Geliştirme** yolu takip edilerek veya uç birimde **lider-console** yazılarak **LiderArayüz**'e erişilebilir.

``` Not: Yukarıdaki şekilde kurulum yapıldı ise aşağıdaki adımları uygulamanız gerekmemektedir!```

##Lider Depodan Kurulum

Pardus bilgisayarlarda aşağıdaki adres tanımlanarak  depodan yüklenebilmektedir. Bu deponun sisteminize tanımlanması için uçbirim(konsol)da;

	sudo wget http://repo.liderahenk.org/liderahenk-archive-keyring.asc && sudo apt-key add liderahenk-archive-keyring.asc &&  rm liderahenk-archive-keyring.asc

    
komutları ile "**liderahenk-archive-keyring.asc**" key dosyası indirilerek sisteme yüklenmelidir. Ardından;

	sudo add-apt-repository 'deb [arch=amd64] http://repo.liderahenk.org/liderahenk stable main'

komutu ile depo adresi "**/etc/apt/sources.list**" dosyasına eklenir. 

``` 
Not: Yukarıdaki adımı uçbirimde bir metin editörü(vi,nano,pico) kullanarak ;

	deb [arch=amd64] http://repo.liderahenk.org/liderahenk stable main

satırını "**/etc/apt/sources.list**" dosyasına elinizle de tanımlayarak yapabilirsiniz. 
```
Daha sonra;

	sudo apt update
    
komutu ile güncel paket listesini alınmalıdır. Uçbirimde;

	sudo apt install lider-console
    
komutu ile LiderArayüz'ü yükleyebilirsiniz. Daha sonra **Uygulamalar Menüsü > Geliştirme** yolu takip edilerek veya uç birimde **lider-console** yazılarak **LiderArayüz**'e erişilebilir.