Semantik Versiyonlama 2.0.0
==============================

Özet
-------

Versiyon numarası MAJOR.MINOR.PATCH olarak verildiğinde:

1. Uyumsuz API değişikliklerinde MAJOR versiyonu,
2. Geriye dönük uyumlu şekilde fonksiyonellik eklendiğinde MINOR versiyonu,
3. Geriye dönük uyumlu hata düzeltmelerinde PATCH versiyonu artırın.

Önceki sürüm ve yapı metası için ek etiketler, MAJOR.MINOR.PATCH formatının
eklentileri olarak mevcuttur.

Giriş
------------

Yazılım yönetimi dünyasında “bağımlılık cehennemi” denilen dehşet bir yer vardır.
Sisteminiz büyüdükçe ve yazılımınıza daha çok paket ekledikçe bir gün kendinizi
bu umutsuzluk içinde bulmanız muhtemeldir.

Çok bağımlı sistemlerde, yeni paket sürümlerini sunmak bir kâbus haline çok
çabuk gelebilir.  Eğer bağımlılık özellikleri çok sıkıysa, versiyon kilitlenmesi
(her bağımlı paketin yeni sürümlerini sunmaya gerek kalmadan bir paketi
geliştirememe) tehlikesindesiniz. Eğer bağımlılıklar çok gevşek belirlenirse,
versiyon karmaşıklığı tarafından ısırılmanız kaçınılmazdır (daha ileri versiyonlar
ile uyumluluğun makul olduğu farzedilerek). Bağımlılık cehennemi, versiyon
kilitlenmesi ve/veya karmaşıklığının sizin kolay ve güvenli şekilde projenizi
ileriye taşımanızı önleyen yerdir.

Bu probleme çözüm olarak, versiyon numaralarının nasıl atandığı ve artırıldığını
prensip edinen basit kurallar ve gereksinimler dizisini öneriyorum. Bu kurallar,
açık ve kapalı kaynaklı yazılımın her ikisinde de, kullanımdaki önceden var olan
genel yaygın yöntemlere bağlıdır fakat bununla sınırlı değildir. Bu sistemin
çalışması için ilk olarak bir genel API bildirmelisiniz. Bu dokümantasyondan
oluşabilir ya da kodun kendisi tarafından uygulanabilir. Ne olursa olsun,
bu API’nin açık ve kesin olması önemlidir. Genel API’nizi tanımladıktan sonra,
versiyon numaranızda belirli artırmalarla değişiklikleri ona iletirsiniz. X.Y.Z
versiyon formatını düşünün(Major.Minor.Patch). API’yi etkilemeyen hata
düzeltmeleri patch versiyonu artırır, geriye dönük uyumlu API eklemeleri/değişimleri
minör versiyonu artırır ve geriye dönük uyumsuz API değişimleri majör
versiyonu artırır.

Bu sisteme “Semantik Versiyonlama” diyorum. Bu plana göre, versiyon numaraları ve
değişme şekilleri, altında yatan kod ve bir versiyondan diğerine neyin
değiştiği hakkında anlam taşır.


Semantik Versiyonlama Tanımı (SemVer)
------------------------------------------

Bu dökümandaki anahtar kelimeler(“MUST-Yapılmalı-Gereklilik”,
“MUST NOT-Yapılmamalı-Yasak”, “REQUIRED-Gerekli”, “SHALL-Yapılmalı-Öneri”,
“SHALL NOT-Yapılmamalı-Öneri”, “SHOULD-Yapılmalı-Öneri”,
“SHOULD NOT-Yapılmamalı-Öneri”, “RECOMMENDED-Önerilir”, “MAY-Yapılabilir”,
“OPTIONAL-İsteğe Bağlı”), [RFC 2119](http://tools.ietf.org/html/rfc2119)’da
belirtildiği gibi yorumlanır.

1. Semantik Versiyonlama kullanan yazılımlar bir genel API bildirmelidir(MUST).
Bu API kodun içinde de bildirilebilir veya tam olarak dokümantasyonda da var
olabilir. Nasıl olursa olsun, kusursuz ve kapsamlı olmalıdır.

2. Normal bir versiyon numarası X.Y.Z (X,Y ve Z negatif olmayan tam sayılar)
formatında olmalı(MUST) ve başında sıfırlar olmamalıdır(MUST NOT). X majör versiyon,
Y minör versiyon ve Z patch versiyondur. Her eleman sayısal olarak artmalıdır(MUST).
Örneğin: 1.9.0 -> 1.10.0 -> 1.11.0.

3. Versiyonlaşmış bir paket yayınlandığında, o versiyonun içeriği
değiştirilmemelidir (MUST NOT). Değişiklikler yeni bir versiyon olarak
yayınlanmalıdır (MUST).

4. Sıfır majör versiyonu (0.y.z) başlangıç geliştirme içindir. Her an  her şey
değişebilir. Genel API kararlı olarak düşünülmemelidir.

5. 1.0.0 versiyonu genel API’yi tanımlar. Bu yayımdan sonraki versiyon numarası
artırımları bu genel API’ye ve nasıl değiştiğine bağlıdır.

6. Z patch versiyonu (x.y.Z | x > 0) yalnızca geriye dönük uyumlu hata düzeltmeleri
tanıtıldığında artırılmalıdır(MUST). Hata düzeltme, yanlış davranışı düzelten iç
değişiklik olarak tanımlanır.

7. Y minör versiyonu (x.Y.z | x > 0) yeni, geriye dönük uyumlu fonksiyonellik genel
API’ye tanıtılırsa artırılmalıdır(MUST). Herhangi bir genel API fonksiyonelliği
“önerilmeyen” olarak işaretlenirse artırılmalıdır(MUST). Özel kod içinde önemli
yeni fonksiyonellik veya gelişmeler tanıtılırsa artırılabilir(MAY). Patch seviye
değişimleri içerebilir(MAY). Minör versiyon artırıldığında, patch versiyonu
sıfırlanmalıdır (MUST).

8. X majör versiyonu (X.y.z | X > 0) herhangi geriye dönük uyumsuz değişiklikler
genel API’ye tanıtıldığında artırılmalıdır(MUST). Minör ve patch seviye değişimleri
içerebilir(MAY). Majör versiyon artırıldığında, patch ve minör versiyon
sıfırlanmalıdır(MUST).

9. Önceki sürüm versiyonu, patch versiyonunu takip eden bir tire ve noktalarla
ayrılmış tanımlayıcılar serisi ekleyerek belirtilebilir(MAY). Tanımlayıcılar
sadece ASCII alfa nümerikler ve tire [0-9A-Za-z-] içerebilir(MUST). Tanımlayıcılar
boş olmamalıdır(MUST NOT). Nümerik tanımlayıcılar başta sıfır içermemelidir(MUST NOT).
Önceki sürüm versiyonları, ilgili normal versiyondan daha az önceliğe sahiptir.
Önceki sürüm versiyonları, versiyonun kararsız olduğunu ve ilgili normal versiyon
tarafından belirtilen, istenilen uyumluluk gereksinimlerini taşıyamayabileceğini
belirtir. Örnekler: 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7, 1.0.0-x.7.z.92.

10. Yapı metası, patch veya önceki sürüm versiyonunu takip eden bir artı işareti
ve noktalarla ayrılmış tanımlayıcılar serisi ekleyerek belirtilebilir(MAY).
Tanımlayıcılar sadece ASCII alfa nümerikler ve tire [0-9A-Za-z-] içerebilir(MUST).
Tanımlayıcılar boş olmamalıdır(MUST NOT). Yapı metası, versiyon önceliği belirlenirken
ihmal edilmelidir(SHOULD). Böylece, sadece yapı metasında farklılık gösteren iki
versiyon aynı önceliğe sahiptir. Örnekler: 1.0.0-alpha+001, 1.0.0+20130313144700,
1.0.0-beta+exp.sha.5114f85.

11. Öncelik, versiyonların sıralandığında nasıl karşılaştırıldığı anlamına gelir.
Öncelik, versiyonu sırasıyla majör, minör, patch ve önceki sürüm tanımlayıcılarına
ayırarak hesaplanmalıdır(MUST)(Yapı metasının önceliğe etkisi yoktur).
Öncelik belirlenirken soldan sağa doğru tanımlayıcılar arasındaki ilk fark belirlenir.
Majör, minör ve patch versiyonları her zaman nümerik olarak karşılaştırılır.
Örnek: 1.0.0 < 2.0.0 < 2.1.0 < 2.1.1. Majör, minör ve patch eşitken önceki sürüm
versiyonu normal versiyondan düşük önceliğe sahiptir. Örnek: 1.0.0-alpha < 1.0.0.
Aynı majör, minör ve patch versiyonuna sahip iki önceki sürüm versiyonlarının önceliği,
bir fark bulunana kadar soldan sağa noktalarla ayrılmış her tanımlayıcıyı
karşılaştırarak belirlenmelidir(MUST). Sadece rakamlardan oluşan tanımlayıcılar
nümerik olarak karşılaştırılır; harf ve tireli tanımlayıcılar ASCII sıralama
düzeninde sözlüksel olarak karşılaştırılır. Nümerik tanımlayıcılar nümerik olmayan
tanımlayıcılardan her zaman daha düşük önceliğe sahiptir. Eğer bütün önceki
tanımlayıcılar eşitse, daha büyük önceki sürüm alanları dizisi daha küçüğüne
göre yüksek önceliğe sahiptir.  Örnek: 1.0.0-alpha < 1.0.0-alpha.1
< 1.0.0-alpha.beta < 1.0.0-beta < 1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0.

Neden Semantik Versiyonlama Kullanıyoruz?
----------------------------

Bu, bir yeni fikir veya devrim değil. Aslında, muhtemelen siz buna benzer bir şey
yaptınız zaten. “Benzer” olan bu problem o kadar da iyi değil. Bazı resmi
tanımlamalar olmadan, versiyon numaraları bağımlılık yönetimi için aslında
gereksizdir. Yukarıdaki fikirlere bir isim ve açık tanımlama vererek, yazılımınızın
kullanıcılarına amaçlarınızı bildirmek kolay hale gelir. Bu amaçlar açık olduğunda,
esnek bağımlılık tanımlamaları nihayet yapılabilir.

Basit bir örnek, Semantik Versiyonlamanın, bağımlılık cehennemini nasıl tarihe
gömdüğünü gösterecek. “İtfaiye” isimli bir kütüphane düşünün. “Merdiven”
isimli bir Semantik olarak versiyonlanan pakete ihtiyaç duyar. İtfaiye
oluşturulduğu zaman, Merdiven’in versiyonu 3.1.0’dır. İtfaiye, ilk defa 3.1.0’da
tanıtılan bazı işlevsellikleri kullandığı için, güvenilir olarak Merdiven bağımlılığını
3.1.0’dan büyük veya eşit fakat 4.0.0’dan küçük olarak belirleyebilirsiniz.
Merdiven versiyonu 3.1.1 ve 3.2.0 çıktıkça, paket yönetim sisteminize ekleyebilirsiniz
ve bilirsiniz ki mevcut bağımlı yazılımla uyumlu olacaktır.

Sorumlu bir geliştirici olarak, herhangi paket güncellemesinin tanıtıldığı gibi
çalıştığını elbette ki doğrulamak isteyeceksiniz. Gerçek dünya karmakarışık bir yerdir;
yapacak bir şey yok fakat uyanık olun. Yapacağınız şu ki; Semantik Versiyonlama’nın,
bağımlı paketlerin yeni versiyonlarını çevirmek zorunda kalmadan paket yayınlama ve
geliştirmeyi makul bir yolla size sunmasına izin verin; zaman ve iş gücünden kazanın.

Eğer bütün bunlar çekici geliyorsa, Semantik Versiyonlama’yı kullanmaya başlamak
için tüm yapmanız gereken, yaptığınızı ilan etmek ve sonra kuralları takip etmek.
BENİ OKU dosyanızdan bu siteye link verin, böylece diğerleri kuralları öğrenir
ve onlardan istifade ederler.

SSS (Sıkça Sorulan Sorular)
---

### 0.y.z ilk geliştirme aşamasında revizyonlarla nasıl ilgilenebilirim?

En basit mantık, ilk geliştirme sürümünü 0.1.0 ile başlatmak ve minor versiyonu
sonraki her sürüm için artırmaktır.

### 1.0.0’ı ne zaman çıkaracağımı nasıl anlarım?

Eğer yazılımın üretimde kullanılıyorsa, büyük olasılıkla zaten 1.0.0 olmalıdır.
Eğer kullanıcılardan gelen bir dengeli API varsa, 1.0.0 olmalıdır. Eğer geriye
doğru uyumluluk hakkında çok endişe ediyorsanız, muhtemelen 1.0.0 olmalıdır.

### Bu hızlı gelişme ve hızlı yineleme yıldırıcı değil mi?

Major sürüm sıfır, her alanda hızlı bir gelişmedir. Eğer API’yi her gün
değiştirirseniz, ya versiyon 0.y.z olmalıdır ya da bir sonraki major sürümü
üzerinde çalışan ayrı bir geliştirme dalı oluşmalıdır.

### Eğer genel API dahil en küçük değişiklikler bile uyumlu bir yumru gerektiriyorsa, bu sürümler 42.0.0’a kadar sona ermeyecek mi?

Bu sorumlu bir gelişme ve öngörü bir sorudur. Uyumsuz değişiklikler için bağımlı
bir kod yeri vardır ve yazılım kolayca tanıtılmamalıdır. Yükseltmek için
gerçekleştirilmiş olmalıdır ve maliyeti önemli olabilir. Uyumsuz değişiklikleri
yayınlamak için büyük sürümleri çarpmak, size değişikliklerin etkisini düşünmeye
ve ilgili maliyet / fayda oranını değerlendirmek anlamına gelir.


### Tüm genel API’nin belgelenmesi çok fazla iş!

Bu başkaları tarafından kullanılmak üzere tasarlanmıştır, yazılım belgelemek
profesyonel bir geliştirici olarak sizin sorumluluğunuzdadır. Yazılım karmaşıklığını
yönetmek, bir projeyi verimli tutmanın oldukça önemli bir parçasıdır ve kimse
hangi yazılımın veya metodların daha güvenli olduğunu bilemez. Uzun vadede,
Semantik Versiyonlama, iyi tanımlanmış bir genel API ısrarı ile herkes
tarafından tutabilir ve her şey sorunsuz çalışabilir.

### Yanlışlıkla minor bir versiyonu geriye uyumsuz değişiklikler olarak yayınlanırsam ne yapmalıyım?

En kısa sürede size Semantik Versiyonlama tekniklerini  kırdığınız gibi,
sorunu çözmek ve sorunu gidermek için, geriye dönük uyumluluk için geri
yeni bir alt sürüm bırakın. Hatta bu surette, bu sürüm bültenlerini
değiştirmek kabul edilemez. Eğer uygunsa, soruna neden olan sürümü
belgeleyin ve soruna neden olan sürüm hakkında kullanıcıları bilgilendirin.

### Genel API’yi  değiştirmeden kendi bağımlılıkları güncellemek için ne yapmam gerekir?

Bu genel API’yi etkilemez çünkü bu uyumlu olarak düşünülebilir. Yazılım açıkça paket
aynı bağımlılıklara bağlıdır ve kendi bağımlılık özellikleri olmalıdır ve yazar
herhangi bir çatışma fark edecektir. Değişikliği bir yama seviyesi ya da küçük
düzeyde değişiklik olup olmadığını belirlemek eğer bir hata düzeltmek veya yeni
işlevler tanıtmak için sizin bağımlılıkları güncellenen bağlıdır. Ben genellikle
açıkça küçük düzeyde artış var bu durumda, ikinci örneğin ek kod beklenebilir.

### Ben yanlışlıkla sürüm numarasını değişim (kod yanlış bir yama sürümü önemli bir kırılma değişiklik tanıttı yani) ile uyumlu olmayan bir şekilde Genel API değiştirmeniz

En iyi kararı kullanın. Büyük ölçüde ortak API istediği her şeyi geri davranışı
değiştirerek etkiledi olacak büyük bir seyirci varsa, o zaman düzeltme kesinlikle
bir yama sürümü kabul edilebilir olsa da, bir büyük sürüm yapmak iyi olabilir.
Unutmayın, Semantik sürüm tüm nasıl sürüm numarasını değişikliklerden anlamı
taşıma ilgilidir. Bu değişikliklerin kullanıcılara önemli ise,
onları bilgilendirmek için sürüm numarasını kullanın.


### Desteklenmeyen işlevsellikleri nasıl takip edebilirim?

Mevcut işlevselliği desteklemeyen yazılım geliştirme normal bir parçasıdır ve
genellikle ileri ilerleme için gereklidir. Eğer ortak API parçası itiraz
edeceğiniz zaman, iki şey yapmanız gerekir: (1), kullanıcıların değişimi, (2)
yerinde desteklenmeme ile yeni bir sürüm olan Pardus sorunu hakkında bilgi
vermek belgeleri güncelleştirmesi. Tamamen yeni bir büyük sürümde
işlevselliği çıkarmadan önce desteklenmeme içeren en az bir ara sürümü
olması gerektiğini kullanıcıların yeni API geçiş sorunsuz yapabilirsiniz kadar.

### Semver sürüm dizesinin bir boyut sınırı var mı?

Hayır, ama iyi değerlendirmelerinizi kullanın. Bir 255 karakter sürümü dizesi
örneğin, muhtemelen gereğinden fazla. Ayrıca, belirli sistemler dize
boyutuna kendi sınırlarını getirebilir.

Hakkında
-----

Semantik Versiyonlama tanımlamasını, Gravatars’ın mucidi ve GitHub’ın kurucularından
[Tom Preston-Werner](http://tom.preston-werner.com) yazmaktadır.

Geri bildirim yapmak istiyorsanız lütfen
[Github'da bir konu açın](https://github.com/mojombo/semver/issues).


Lisans
-------

Creative Commons - CC BY 3.0
[http://creativecommons.org/licenses/by/3.0/](http://creativecommons.org/licenses/by/3.0/)

