**Kayıt Şablonları**

Şablonda belirtilen metinle başlayan istemcilerin domaine sadece şablonda belirtilen gruba üye olan 
kullanıcılar tarafından alınmasını sağlayıp bu kullanıcıların şablonda verilen Organizasyon Birimi altında 
oluşturulmasını sağlar. Örneğin şablon adı:

>'pardus-01-', yetkili grup DN'i 'cn=adminGroups,ou=User,ou=Groups,dc=liderahenk,dc=org'

ve istemcilerin dahil edileceği Organizsayon Birimi ise: 

>'ou=ANKARA,ou=Agents,dc=liderahenk,dc=org'

olsun. 

Bu kayıt şablonundan sonra istemci adı: 
'pardus-01-' ile başlayan tüm kullanıcılar sadece: 

>'cn=adminGroups,ou=User,ou=Groups,dc=liderahenk,dc=org'

grubunda yer alan yetkili kullanıcılar tarafından domaine alınabilir ve domaine alınan istemciler 

>'ou=ANKARA,ou=Agents,dc=liderahenk,dc=org' 

Organizsayon Birimi altında oluşturulur.

![Dosya Paylaşımı](../images/registirationTemplate/registirationTemplate.png#zoom)



<a href="../../images/registirationTemplate/registirationTemplate.png" class="without-caption image-link">
  <img src="../../images/registirationTemplate/registirationTemplate.png"  />  
</a>
<br/>
<a href="../images/registirationTemplate/registirationTemplate.png" data-source="http://commons.wikimedia.org/wiki/Commons:Picture_of_the_day" class="with-caption image-link" title="The caption">
  <img src="../images/registirationTemplate/registirationTemplate.png"  />  
</a>

<br/>


<style>

.image-link {
  cursor: -webkit-zoom-in;
  cursor: -moz-zoom-in;
  cursor: zoom-in;
}


/* This block of CSS adds opacity transition to background */
.mfp-with-zoom .mfp-container,
.mfp-with-zoom.mfp-bg {
	opacity: 0;
	-webkit-backface-visibility: hidden;
	-webkit-transition: all 0.3s ease-out; 
	-moz-transition: all 0.3s ease-out; 
	-o-transition: all 0.3s ease-out; 
	transition: all 0.3s ease-out;
}

.mfp-with-zoom.mfp-ready .mfp-container {
		opacity: 1;
}
.mfp-with-zoom.mfp-ready.mfp-bg {
		opacity: 0.8;
}

.mfp-with-zoom.mfp-removing .mfp-container, 
.mfp-with-zoom.mfp-removing.mfp-bg {
	opacity: 0;
}



/* padding-bottom and top for image */
.mfp-no-margins img.mfp-img {
	padding: 0;
}
/* position of shadow behind the image */
.mfp-no-margins .mfp-figure:after {
	top: 0;
	bottom: 0;
}
/* padding for main container */
.mfp-no-margins .mfp-container {
	padding: 0;
}



/* aligns caption to center */
.mfp-title {
  text-align: center;
  padding: 6px 0;
}
.image-source-link {
  color: #DDD;
}


body { -webkit-backface-visibility: hidden; padding: 10px 30px; 
  font-family: "Calibri", "Trebuchet MS", "Helvetica", sans-serif;
}

</style>

<script>

$('.without-caption').magnificPopup({
		type: 'image',
		closeOnContentClick: true,
		closeBtnInside: false,
		mainClass: 'mfp-no-margins mfp-with-zoom', // class to remove default margin from left and right side
		image: {
			verticalFit: true
		},
		zoom: {
			enabled: true,
			duration: 300 // don't foget to change the duration also in CSS
		}
	});

$('.with-caption').magnificPopup({
		type: 'image',
		closeOnContentClick: true,
		closeBtnInside: false,
		mainClass: 'mfp-with-zoom mfp-img-mobile',
		image: {
			verticalFit: true,
			titleSrc: function(item) {
				return item.el.attr('title') + ' &middot; <a class="image-source-link" href="'+item.el.attr('data-source')+'" target="_blank">image source</a>';
			}
		},
		zoom: {
			enabled: true
		}
	});



</script>