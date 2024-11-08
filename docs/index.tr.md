<div align="top">
  <div style="display: flex;">&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;
    <img style="width: 95%; height: 55%" src="./images/yeni logo kullanımı.png" class="img-fluid" alt="">&nbsp; &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp;
  </div>
</div>

## Liderahenk Merkezi Yönetim Sistemi

Liderahenk Merkezi Yönetim Sistemi
Kurumsal ağ üzerindeki sistemleri ve kullanıcıları merkezden yönetilebilmeyi, izlemeyi 
ve denetlemeyi sağlayan, açık kaynaklı bir yazılım sistemidir.

### Neden Liderahenk?

Açık kaynak kodlu olması sayesinde daha güvenli, kaliteli, esnek, izlenebilir ve kolay geliştirilebilir 
yapıdadır. Kullanıldıkça büyüyen geliştirici topluluğu ile daha güçlü destek ve toplam sahip olma maliyeti 
avantajı sağlar. Yerel ya da dağıtık LDAP tabanlı çözüm altyapısı ile bilgisayar ve kullanıcıyı yönetir. 
Sistemin tümünü ya da belirli nitelikteki donanım ve kullanıcı kümelerini ayrı ayrı ya da toplu halde 
yönetmek üzere ölçeklenebilir çözüm sağlar.

### Bileşenler

1. **Lider**

	Merkezde toplanan verilerin saklanması, tanımlanan politikaların ve verilengörevlerin istemcilere dağıtılmasından sorumlu sistemin temel bileşenidir.

2. **Ahenk**

	Lider'den iletilen görevleri yerine getirmek, politikaları uygulamak ve sonuçlarını Lider'e iletmekten sorumlu servis yazılımıdır. Ahenk yönetilen sistemlerde tam yetkili (super user) olarak çalışmaktadır.

3. **Lider Arayüz**

	İstemci ve kullanıcı yönetimi işlemlerinin yapıldığı arayüzdür. Görev ve kullanıcı politikalarının tanımlanması, sunucu ayarlarının yapılması, raporlama gibi bir çok işlemler bu arayüz aracılığı ile yapılmaktadır.

### Yetenekler
1. **Görev**

	İstemci ya da istemci grubuna doğrudan gönderilen ve Ahenk kurulu istemciler üzerinde çalıştırılan anlık işlerdir. Ahenk yüklü istemci aktif durumda ise gönderilen görev anında uygulanır. Genellikle bağımsız işlemler için geliştirilen eklentiler tarafından kullanılır. Zamanlanmış görev özelliği ile belirlenen zaman diliminde gönderilen görevi çalıştırılması sağlanır. Ayrıca oluşturulan bu zamanlanmış görevler güncellenebilmekte veya iptal edilebilmektedir. Kaynak kullanımı, paket(uygulama) yönetimi, yerel kullanıcı yönetimi, betik çalıştır, servis yönetimi, dosya transferi, usb yönetimi gibi özellikleri içerir.

2. **Profil**

	Bir eklentide gerçekleştirilebilecek yapılandırma ayarlarının bütününü ifade eder. Bir veya birden fazla profil bir araya gelerek politikayı oluşturur. Tek başına kullanıcı odaklı çalıştırılamaz. Bir politika üzerine eklendikten sonra kullanılabilir. İnternet taracıyı profili, betik profili, usb profili, mesaj profili, oturum yönetimi profili gibi özellikleri içerir.

3. **Politika**

	Bir ya da daha fazla çalıştırılabilen profillerin bir araya gelmesi ile oluşturulur. Politika ile eklentilerin sağladığı imkanların-kısıtlamaların bir kitlenin özelliklerine göre işletilmesi sağlanabilir. Kullanıcı grubuna uygulanırlar. Politika kullanıcı grubuna atandıktan sonraki ile kullanıcı oturumu açması esnasında Lider'den sorgulanarak uygulanır.

4. **Raporlar**

	Liderahenk Merkezi Yönetim Sistemine kayıt olan istemcilere ait detaylı arama yapılarak rapor alınabilmekte ve arama sonuçlarına göre İstemci Grubu oluşturulabilmektedir. Lider üzerinde istemcilere gönderilen görev detayları sorgulabilmektedir. Ayrıca Zamanlanmış olarak gönderilen görevlere ait rapor oluşturulabilmekte, tekrar düzenlenebilmekte ve iptal edilebilmektedir.


<link href="/lider3.0/assets/style.css" rel="stylesheet"></link>

