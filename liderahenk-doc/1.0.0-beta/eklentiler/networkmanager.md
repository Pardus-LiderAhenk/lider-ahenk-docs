# Ağı Yönet Eklentisi

Eklenti görev şeklinde çalışmaktadır. Herhangi bir Ahenk üzerine uygulandığında o Ahenk üzerindeki ağ ayarlarını okuyarak ekrana getirir.

![Network](images/network-mevcut-konfigurasyon.png)

Ahenk üzerinde daha önce tanımlanmış olan dns konfigürasyonuna **"DNS"** sekmesinden erişilebilir.

![Network](images/network-dns.png)

**"Ekle"** simgesine tıklanarak yeni bir dns tanımlanabilir. Bu ekranda belirlenen dns ip adresi tanımlandıktan sonra  dns ayarının aktif-pasifliği belirlenebilir.

![Network](images/network-yeni-dns.png)

**"Çalıştır"** simgesine tıklanarak yeni dns adresi Ahenk üzerine uygulanabilir.

![Network](images/network-yeni-dns-1.png)

Ekran kapatılarak yeniden **"Ağı Yönet"** denilerek girilen dns adreslerinin Ahenk üzerinde bulunduğu kontrol edilebilir. Tanımlanan dns **"Sil"** simgesine tıklanarak kaldırılabilir.

![Network](images/network-yeni-dns-2.png)

Ahenk üzerinde **"/etc/hosts"** adresinde daha önce tanımlı olan sunucu adresleri **"Sunucular"** ekranında görülebilir. 

![Network](images/network-sunucular-1.png)

**"Ekle"** simgesi ile yeni  sunucu(ların) tanımlaması yapılabilir.

![Network](images/network-sunucular-2.png)

Yine Ahenk üzerinde **"/etc/hostname"** altında tutulan makine adı **"Genel"** sekmesinden değiştirilebilir. Yeni sunucu adı girildikten sonra **"Değiştir"** simgesi ile yeni makine adı Ahenk üzerine uygulanır.

![Network](images/network-genel.png)

Ekran kapatılarak yeniden **"Ağı Yönet"** denilerek girilen makine  adının Ahenk üzerinde değiştiği kontrol edilebilir.

![Network](images/network-genel-1.png)

**"Ağ Ayaları"** sekmesi ile Ahenk üzerine yeni bir ağ ayarı yapışlandırması yapılabilir.

![Network](images/network-agayarlar.png)

 **"Ekle"** simgesine tıklandığında gelen ekranda **"Tip"** değeri ile ağın **"STATIC"**,**"LOOPBACK"** ve **"DHCP"** seçimi yapılır. Seçime göre alt değerlerin düzenleme seçeneği aktif-pasif olur.
 
![Network](images/network-yeni-agarayuzu.png)

Bu ekrana gerekli değerler girilerek **"Çalıştır"** simgesine tıklanmalıdır.
