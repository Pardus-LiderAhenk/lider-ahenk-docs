# Güvenlik Duvarı Eklentisi

Varolan güvenlik duvarı kurallarını getirmeyi ve yeni güvenlik duvarı kuralları tanımlamayı sağlayan bir eklentidir. Eklenti, hem görev hem de politika özelliğine sahiptir.

Görev tarafında, eklenti ekranının açılmasıyla birlikte ilgili Ahenk makinesindeki güvenlik duvarı kuralları getirilir. Bu ekran üzerinde herhangi bir düzenleme yapılamaz. Yeni güvenlik duvarı kuralı eklemek için eklentinin politika tarafını kullanmak gereklidir.

![Firewall Eklenti](https://github.com/Pardus-LiderAhenk/lider-ahenk-docs/blob/master/1.0.0/images/firewall-eklenti.png)

Eklentinin politika tarafında uygulanmak istenen güvenlik duvarı kuralı/kuralları COMMIT ifadesinden önce belirtilir. Bir örnekle açıklamak gerekirse;


****filter**

**:INPUT ACCEPT [9:927]**

**:FORWARD ACCEPT [0:0]**

**:OUTPUT ACCEPT [3:378]**

**uygulanmak_istenen_firewall_kuralı**

**COMMIT**


ifadesi güvenlik duvarı kuralını uygulamak için yeterli olacaktır.

![Firewall Politika](https://github.com/Pardus-LiderAhenk/lider-ahenk-docs/blob/master/1.0.0/images/firewall-politika.png)

**:INPUT, :FORWARD** ve **:OUTPUT** ifadeleriyle başlayan kısımlar görev esnasında getirilen güvenlik duvarı kurallarının **:INPUT, :FORWARD** ve **:OUTPUT** ifadeleriyle başlayan kısımlarının aynısıdır.
