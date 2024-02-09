**Sunucu Bilgileri**

Sunucu bilgileri kısmında sunucularınızı ekleyerek sunucuların bilgilerini görebilirsiniz. Sunucuların bilgilerini alabilmeniz için sunucuların ssh bağlatıları açık olmalı ve üzerinde Osquery kurulu olması gerekiyor.

[![Sunucu Bilgileri](../images/serverInformations/serverInformationAccess.png)](../images/serverInformations/serverInformationAccess.png)

Eklediğiniz makinelere ait bilgileri aşağıdaki gibi görebilirsiniz. Makinelere ait
listeleme ekranında; ip adresi, işletim sistemi bilgisi, makinenin durumu ve makineye ait detaylar bulunuyor. Kullanıcı loglarında ise makinenin ismi, uptime süresi ve açıklamanız yer almaktadır. Makinenin disk, ram ve cpu bilgileride bulunmaktadır.

**Osquery Kurulum:**
Osquery, açık kaynaklı sistem yönetimi aracıdır. Osquery ile sql tabanlı sorgulama dilini kullanarak bilgisayarınız hakkında bilgi toplayabilirsiniz.

Osquery paketi işletim sisteminizin üzerinde yoksa osquery paketini indirip kurmanız gerekmektedir;

- wget https://pkg.osquery.io/deb/osquery_4.6.0-1.linux_amd64.deb
- sudo dpkg -i osquery_4.6.0-1.linux_amd64.deb

Bilgisayarınızda Osquery paketi mevcutsa;  

- sudo apt update
- sudo apt install osquery

Debian tabanlı işletim sistemleri için Osquery kurulumu bu şekildedir.

[![Sunucu Bilgileri List](../images/serverInformations/serverInformationsList.png)](../images/serverInformations/serverInformationsList.png)

Eklenilenilen makinede ssh bağlantısı ve Osquery kurulu olduğunda aşağıdaki gibi detaylar bölümü yer almaktadır.

[![Sunucu Bilgileri Detail](../images/serverInformations/serverInformationDetail.png)](../images/serverInformations/serverInformationDetail.png)

Eklendiğiniz makineleri silebilir ve güncelleyebilirsiniz.

[![Sunucu Bilgileri Delete](../images/serverInformations/serverInformationDelete.png)](../images/serverInformations/serverInformationDelete.png)

[![Sunucu Bilgileri Update](../images/serverInformations/serverInformationUpdate.png)](../images/serverInformations/serverInformationUpdate.png)