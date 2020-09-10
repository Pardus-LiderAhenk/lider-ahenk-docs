**Ahenk Kayıt**

Ahenk paketi "repo.liderahenk.org" adresinde sunulmaktadır. Pardus bilgisayarlarda bu adres tanımlanarak ahenk paketi 
depodan yüklenebilmektedir. Bu deponun sisteminize tanımlanması için uçbirim(konsol)da;

    sudo wget http://repo.liderahenk.org/liderahenk-archive-keyring.asc && sudo apt-key add liderahenk-archive-keyring.asc &&  rm liderahenk-archive-keyring.asc
    
komutları ile "liderahenk-archive-keyring.asc" key dosyası indirilerek sisteme yüklenmelidir. Ardından;

    sudo printf  "deb [arch=amd64] http://repo.liderahenk.org/liderahenk stable main" | sudo tee -a /etc/apt/sources.list
    
komutu ile depo adresi "/etc/apt/sources.list" dosyasına eklenir.

Not: Test reposu için aşağıda belirtilen komut çalıştırılmalıdır.
    
    sudo printf  "deb [arch=amd64] http://repo.liderahenk.org/liderahenk-test testing main" | sudo tee -a /etc/apt/sources.list

Not: Yukarıdaki adımı uçbirimde bir metin editörü(vi,nano,pico) yardımı ile ;

    deb [arch=amd64] http://repo.liderahenk.org/liderahenk stable main

satırını "/etc/apt/sources.list" dosyasına elinizle de tanımlayabilirsiniz.

Daha sonra;

    sudo apt update
    
komutu ile güncel paket listesini alınmalıdır.

    sudo apt install ahenk
    
komutu ile güncel Ahenk versiyonu indirilir.    
    
    ahenk-register

komutu ile ahenk çalıştırılır.

![Ahenkregister](./images/ahenkregister.jpeg)

Açılan pencereden Evet butonuna tıklanır ve kuruluma devam edilir.

![Ahenkregister](./images/ahenkregisterinfo.jpeg)

Gerekli bilgiler girildikten sonra Tamam butonuna tıklayarak kurulum başlatırlır.

![Ahenkregister](./images/hosgeldiniz.jpeg)

Kurulum tamamlandıktan sonra açılan pencereden Tamam butonuna tıklayarak devam edilir.

![Ahenkregister](./images/restart.jpeg)

Kurulum başarılı bir şekilde tamamlanmıştır. Tamam butonuna tıkladıktan sonra bilgisayar yeniden başlatılır.
Bilgisayar domaine alınmıştır.