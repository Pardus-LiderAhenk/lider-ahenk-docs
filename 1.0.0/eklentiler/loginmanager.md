# Oturum Yöneticisi Eklentisi

Kullanıcının/kullanıcıların oturum açabilecekleri zaman dilimleriyle ilgili izinlerini düzenlemek için geliştirilmiştir. Belli bir süreye kadar geçerli olan oturum açılabilecek zaman dilimleri, gün ve saat bazında belirtilir.

Eklenti, hem görev hem de politika özelliğine sahiptir. Görev tarafında, bir Ahenk makinesinde oturum açmış tüm kullanıcıların oturumlarını tek bir tuşla sonlandırmayı sağlar.

![Im154](/images/oturumlari-sonlandir.png)

Politika tarafında kullanıcının/kullanıcıların hangi zaman dilimleri içerisinde oturum- açabileceği beliritilir. Bunun için Son Geçerlilik Tarihi‘ne kadar geçerli olacak bir kural belirlenir. Örneğin resimde, kullanıcının 5 Mart 2018 tarihine kadar haftanın 5 (pazartesi, salı, çarşamba, perşembe, cuma) günü sabah saat 08:00 ile akşam saat 17:12 arasında oturum açabileceği söylenmiştir. Geri kalan zaman diliminde kullanıcı oturum açsa bile 1 dakika içerisinde oturumu sonlandırılacaktır. Yine aynı şekilde, başka bir kural tanımlanmadığı takdirde, Son Geçerlilik Tarihi‘nden sonra kullanıcının oturum açmaya izni olmayacak ve oturumu sonlandırılacaktır.

![Im146](/images/oturum-yonetimi-profil.png)

Eklentide tanımlanan cron görevi yardımıyla kullanıcının izinli olduğu zaman diliminin- dakikada bir kontrol edilmesi sağlanmıştır. Bu durum tek bir kullanıcıya uygulanabileceği gibi tek bir makine üzerindeki bütün kullanıcılara da uygulanabilir.