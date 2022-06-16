#  LiderAhenk OVA

Ova dosyasını [buradan](http://docs.liderahenk.org/lider-ahenk-docs/1.1.0/ova/lider-server-1.1.ova) indirebilirsiniz. Bu Virtualbox dosyası aşağıdaki bilgileri içermektedir. **Virtualbox > Dosya > Aygıtı İçe Aktar** yolu ile içe aktararak kullanabilirsiniz. Bu adım için https://docs.oracle.com/cd/E26217_01/E26796/html/qs-import-vm.html adresinden bilgi alabilirsiniz.

Ova ağ ayarları **"Köprü Bağdaştırıcısı"** şeklinde ayarlanmıştır. Sistem çalıştığında DHCP'den otomatik ip alacaktır. Statik bir ip olması gerekli olduğu için bu ip adresinin ova içerisindeki sisteme tanımlanması gereklidir. Bu işlem için https://wiki.debian.org/NetworkConfiguration adresinden bilgi alabilirsiniz.

**İşletim Sistemi :** Pardus 17.2

**Kullanıcı Adı:** Pardus

**Şifre:** lider


**Donanım**
2 GB Ram
1 CPU
28 GB Disk


**OpenLDAP(Slapd)**

| Kullanıcı	| Şifre |
| ------ | ------ |
|  admin  |  ssifre  |


**Veritabanı(MariaDB)**

| Kullanıcı| Şifre |
| ------ | ------ |
|  root |  msifre  |

**Ejabberd-XMMP**

| Kullanıcı	| Şifre |
| ------ | ------ |
| admin | easifre |
| lider_sunucu | elssifre |

**Lider Console**

| Kullanıcı| Şifre |
| ------ | ------ |
| admin | ssifre |
| lider_console | elcsifre |
| config | csifre |

## Ejabberd Sunucu Ayarları

Ova dosyasını içe aktarma işlemi tamamlandıktan ve sanal sunucu başlatıldıktan sonra;

	systemctl status ejabberd.service
    
komutu ile ejabberd servisinin **active** olduğunu kontrol ediniz, şayet servis aktif değilse;

	systemctl start ejabberd.service

komutu ile servisi aktif hale getiriniz. Daha sonra lider sunucu ayarlarına geçiniz.

## Lider Sunucu Ayarları
 Lider Sunucu için belirlediğiniz sanal makinanın ip adresini satıların başındaki # işaretini kaldırarak;

**/etc/hosts** dosyası altındaki 'ip_adresi' alanına;

```sh
ip_adresi lider.liderahenk.org
ip_adresi ldap.liderahenk.org
ip_adresi ds.liderahenk.org
ip_adresi db.liderahenk.org
ip_adresi im.liderahenk.org 
```

**/opt/lider-distro-1.1/etc/tr.org.liderahenk.cfg** dosyasında 
```sh
xmpp.host = ip_adresi
```
ve 
```sh
file.server.host = ip_adresi
```
tanımlayarak karaf servisi;

```sh
cd /opt/lider-distro-1.1/bin/
./karaf
./start
```

komutları ile başlatılmalıdır.


## Ahenk Kurulumu

Ahenk kurulumu için http://docs.liderahenk.org/lider-ahenk-docs/1.1.0/ahenk/ahenk/#ahenk-kayt adresini ziyaret edebilirsiniz. Kurulum için;

    host = ip_adresi
    receiverjid = lider_sunucu
    receiverresource = Smack
    servicename = im.liderahenk.org

ahenk makinesinde yukarıdaki bilgileri **/etc/ahenk/ahenk.conf** dosyasına tanımlanmalıdır.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bu işlemlerden sonra ahenk bilgisayarda kullanıcı  oturumu kapatılarak yeniden giriş yapılır. **LiderAhenk Kullanıcı Sözleşmesi** onaylanarak devam edilir.

Not: **/etc/ahenk/ahenk.conf** dosyasında;

	agreement = 2
    
şeklinde düzenleme yapıldığı taktirde kullanıcıya yukarıdaki sözleşmenin gele**me**mesi sağlanabilir.

## Lider Console Örnek Bağlantı

Uygulamalar menüsünde veya uçbirimde **lider-console** yazarak LiderArayüz'e erişebilirsiniz. Açılan ekranda **lider-console** bağlantısına tıklanır;

![Lider Console Örnek Bağlantı-1](virtual-ova-images/lider_console.png)

oturum açıldığında (Ekranında sağında) **Sistem Güncesi**'inde **Bağlantı başarıyla açıldı** mesajı gelmelidir. Aksi taktirde bağlantı ve konfigürasyonları kontrol ediniz. Bağlantı başarılı ise **Ahenkler** altında eklenen ahenk bilgisayarlarını görebilirsiniz.

![Lider Console Örnek Bağlantı-2](virtual-ova-images/lider_console-2.png)
