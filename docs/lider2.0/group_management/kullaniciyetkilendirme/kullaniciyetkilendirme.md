**Kullanıcı Yetkilendirme (SUDO)**


![Kayıt Bilgileri](../images/kullaniciyetkilendirme/kayitbilgisi.png)

Bu sayfada kullanıcıların hangi istemcilerde yetkili olacağı ayarlanabilir. Bu işlem için menüden yeni yetki grubu oluştur butonu tıklanır. Ardından çıkan ekrandan en az birer adet olmak üzere 'sudoHost', 'sudoUser' ve 'sudoCommand' özellikleri eklenir.
sudoHost: Hangi istemcilerde verilen yetkininin işleyeceğini gösterir. Bu alana istemci DN adresi eklenmelidir. Birden fazla istemci DN adresi eklenebilir.
sudoCommand: İstemcilerde hangi komutların çalıştırılabileceğini gösterir.(Tüm komutlar için 'ALL' eklenebilir). Birden fazla komut eklenebilir.
sudoUser: Seçilen istemcilerde hangi kullanıcıların yetkili olacağını gösterir. Bu alana kullanıcı DN adresi eklenmelidir.  Birden fazla kullanıcı DN adresi eklenebilir

Bu işlemlerden sonra yetki verilen kullanıcılar eklenen istemcilerde sudoCommand alanında eklenen komutları çalıştırabilirler.

![Grup Üyeleri](../images/kullaniciyetkilendirme/grupuyeleri.png)
<link href=/lider2.0/assets/style.css rel=stylesheet></link>
