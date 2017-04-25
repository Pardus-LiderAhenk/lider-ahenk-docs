# Yedekleme Eklentisi

Dizinlerin yedeklenmesini sağlayan eklentidir.

Eklenti, hem görev hem de politika özelliğine sahiptir.

![Im299](images/Im299)

Kullanıcı Adı, Parola, Hedef IP, Hedef Kapı ve Hedef Dizin alanları doldurulur. SSH- anahtarı kullanılacaksa SSH Anahtarını Kullan seçeneği, LVM Gölgeleme kullanılacaksa

- LVM Gölgeleme Kullan seçeneği seçilir.

Ekleme butonuna basılmasıyla birlikte Yedeklenecek Dizinin nasıl yedekleneceği ile- ilgili ekran açılır. Bu ekranda yedeklenmesi istenilen dizinin yolu yazıldığı gibi eğer harici

- tutulacak dizin varsa bu dizin de Harici Tutulacaklar alanında belirtilir.

![Im307](images/Im307)

![Im314](images/Im314)

- Eklentinin politika tarafı da görev tarafıyla aynı yapıya sahiptir.

- 1.21. Yerel Kullanıcılar Eklentisi

Sisteme yeni kullanıcı ekleme, kullanıcıyı silme ve varolan kullanıcı üzerinde

- değişiklikler yapmak için geliştirilmiştir. Ekleme ve düzenleme ekranlarında kullanıcı adı,

- parola, ev dizini, aktiflik/pasiflik durumu ve kullanıcı grupları alanları yer alır.

Yerel kullanıcılar, bir görev eklentisidir. Dört farklı özelliğe sahiptir: Listeleme,

- Kullanıcı Ekleme, Silme, Düzenleme.

- 1.21.1. Listeleme

![Im321](images/Im321)

- Yerel Kullanıcılar ekranının açılmasıyla birlikte bilgisayar üzerinde bulunan bütün kullanıcılar

- ait oldukları gruplar, ev dizinleri ve aktif olup olmama durumlarıyla birlikte listelenir.

Açılan ekranda üç tane seçenek bulunmaktadır: Ekle, Sil, Düzenle

Ekleme ekranında sisteme yeni bir kullanıcı eklenir. Listeden herhangi bir kullanıcının- seçilip “Sil” butonuna basılmasıyla kullanıcı sistemden silinir. Yine aynı şekilde “Düzenle”

- butonuna basılmasıyla açılan ekranda kullanıcı üzerinde herhangi bir değişiklik yapılabilir.

- Aynı zamanda listedeki kullanıcı üzerine çift tıklamayla da düzenleme ekranı açılabilir.

- 1.21.2. Kullanıcı Ekleme

- Yeni

- kullanıcı eklemek için kullanıcı adı kısıtlarına uyan bir kullanıcı adı, parola ve ev dizini girilir.

- Kullanıcının “Aktif” ya da “Pasif” olacağı belirtilir (Pasif olma durumunda kullanıcının login

- olmasına izin verilmemektedir.). Kullanıcı Grupları kısmı ise opsiyoneldir. Kullanıcı birden

- fazla gruba eklenebileceği gibi hiçbir gruba da eklenmeyebilir.

Gerekli   bütün   bilgiler   yazıldıktan   sonra   “Çalıştır”   butonuna   basılmasıyla   birlikte- kullanıcı sisteme eklenir. Ekleme ekranı kapatıldığında liste yenilenecek ve yeni kullanıcı da

- listede görünecektir.

- 1.21.3. Kullanıcı Düzenleme

![Im328](images/Im328)

![Im335](images/Im335)

- Kullanıcı adını değiştirmek için “Yeni Kullanıcı Adı” alanı doldurulur. Parola kısmı boş

- bırakılırsa kullanıcının önceki parolası değiştirilmeyecektir. Ev dizini, aktiflik/pasiflik durumu

- ve gruplar kısımları da düzenlendikten sonra “Çalıştır” butonuna basılır ve listeleme

- ekranında kullanıcının son durumu görülür.