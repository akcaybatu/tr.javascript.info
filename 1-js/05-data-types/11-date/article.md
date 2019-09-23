# Tarih ve Zaman

Bu konuda yeni bir gömülmüş obje olan [Date](mdn:js/Date) anlatılacaktır. Bu obje tarihi ve saati tutar ve tarih/saat yönetimini üstlenir.

Örneğin, bu objeyi sadece saati saklama, modifiye etme için kullanabilirsiniz, veya zaman ölçümü için veya o anki zamanı göstermek için

## Yaratma

Yeni bir `Date` objesi yaratmak için `new Date()` aşağıdaki argümanların biri ile çağrılabilir.

`new Date()`
: Argümansız -- yeni o anki tarih ve saat ile yeni bir `Date` objesi oluşturur:

    ```js run
    let simdi = new Date();
    alert( simdi ); // o anki tarih/saati gösterir.
    ```

`new Date(milisaniye)`
: 1 Ocak 1970 UCT+0'dan sonra geçen milisaniye(1/1000) ile tarih oluşturulmasıdır

    ```js run
    // `0`  01.01.1970 UTC+0 demektir.
    let Jan01_1970 = new Date(0);
    alert( Jan01_1970 );

    // Buna 24 saat eklemek için, get 02.01.1970 UTC+0
    let Jan02_1970 = new Date(24 * 3600 * 1000);
    alert( Jan02_1970 );
    ```
    1 ocak 1970'den buyana geçen milisaniyeye *timestamp* ( zaman damgası ) denir.
    
    Bu tarihin en basit biçimde gösterimidir. Her türlü bu zaman damgasından yeni bir tarih oluşturmak mümkündür. Veya yine herhangi bir tarihten bu zaman damgasını `date.getTime()` ile almak mümkündür.

<<<<<<< HEAD:1-js/05-data-types/10-date/article.md
`new Date(tarih_metni)`
: Eğer bir argüman var ve bu da karakter dizisi ise, `Date.parse` algoritmasına göre bakılır ve uygunsa tarih oluşturulur.

    ```js run
    let tarih = new Date("2017-01-26");
    alert(tarih); // Thu Jan 26 2017 ...
    ```

`new Date(yıl, ay, gün, saat, dakika, saniye, milisaniye)`
: Yerel zamanda `Date` objesi oluşturmak için sadece ilk iki argüman zorunludur.

    Not:
=======
    An integer number representing the number of milliseconds that has passed since the beginning of 1970 is called a *timestamp*.

    It's a lightweight numeric representation of a date. We can always create a date from a timestamp using `new Date(timestamp)` and convert the existing `Date` object to a timestamp using the `date.getTime()` method (see below).

`new Date(datestring)`
: If there is a single argument, and it's a string, then it is parsed automatically. The algorithm is the same as `Date.parse` uses, we'll cover it later.

    ```js run
    let date = new Date("2017-01-26");
    alert(date);
    // The time is not set, so it's assumed to be midnight GMT and
    // is adjusted according to the timezone the code is run in
    // So the result could be
    // Thu Jan 26 2017 11:00:00 GMT+1100 (Australian Eastern Daylight Time)
    // or
    // Wed Jan 25 2017 16:00:00 GMT-0800 (Pacific Standard Time)
    ```

`new Date(year, month, date, hours, minutes, seconds, ms)`
: Create the date with the given components in the local time zone. Only the first two arguments are obligatory.
>>>>>>> 4d654318ccb6d37d6cefc9b859cf111ff3c96b27:1-js/05-data-types/11-date/article.md

    - `yıl` 4 basamaktan oluşmalıdır. `2013` olur, `98` olmaz.
    - `ay` sıfırdan başlar. Yani `0` Ocak, `11` Aralıktır.
    - `gün` parametresi girilmez ise `1` olarak kabul edilir.
    - `saat/dakika/saniye/milisaniye` değerleri girilmez ise `0` olarak kabul edilir.
    
    Örneğin:

    ```js
    new Date(2011, 0, 1, 0, 0, 0, 0); // // 1 Jan 2011, 00:00:00
    new Date(2011, 0, 1); // Diğer değerler veirlmediği halde yine aynı sonuç alınacaktır.
    ```
    En düşün hassasiyet 1ms'dir(1/1000)

    ```js run
    let tarih = new Date(2011, 0, 1, 2, 3, 4, 567);
    alert( tarih ); // 1.01.2011, 02:03:04.567
    ```

## Tarih bileşenlerine erişim

<<<<<<< HEAD:1-js/05-data-types/10-date/article.md
`Date` objesinde yıla, aya vs. erişim için birçok metod bulunmaktadır. Fakat bunlar kaegorilere ayrılırsa hatırlanması daha kolay olacaktır.
=======
There are methods to access the year, month and so on from the `Date` object:
>>>>>>> 4d654318ccb6d37d6cefc9b859cf111ff3c96b27:1-js/05-data-types/11-date/article.md

[getFullYear()](mdn:js/Date/getFullYear)
: Yılı döner (4 basamaklı)

[getMonth()](mdn:js/Date/getMonth)
: Ayı döner, **0-11 arasında**.

[getDate()](mdn:js/Date/getDate)
: Ayın gününü döner, 1-31 arasındadır. İsmi aklınızı karıştırabilir.

[getHours()](mdn:js/Date/getHours), [getMinutes()](mdn:js/Date/getMinutes), [getSeconds()](mdn:js/Date/getSeconds), [getMilliseconds()](mdn:js/Date/getMilliseconds)
: Sırası ile `saat`, `dakika`, `saniye` ve `milisaniye` bilgilerini döner.

```warn header=" `getYear()` değil `getFullYear()`"

Çoğu JavaScript motoru standart olmayan `getYear()` metodunu entegre etmişlerdir. Bu metod kullanımdan kaldırılmıştır. Bazen iki basamaklı yılı dönerler. Bu metodu kullanmayın!. Bunun yerine `getFullYear()` metodunu kullanabilirsiniz.

```
Bunlara ek olarak haftanın hangi günü olduğu bilgisi de alınabilir:

[getDay()](mdn:js/Date/getDay)
: Haftanın gününü, Pazar `0` ,  Pazartesi `6` olacak şekilde alır. İlk gün her zaman pazardır. Bazı ülkelerde pazar resmi olarak ilk gün olmasa bile bu fonksiyon pazarı yine de ilk gün olarak alır.

**Yukarıdaki tüm metodlar değerlerini yerel saate göre dönerler.**

Bunun uluslararası saat için eşleri mevcuttur(UTC). Bu metodlar gün, ay, yıl vs değerlerini UTC+0'a göre dönerler:
There are also their UTC-counterparts, that return day, month, year and so on for the time zone UTC+0: [getUTCFullYear()](mdn:js/Date/getUTCFullYear),[getUTCMonth()](mdn:js/Date/getUTCMonth), [getUTCDay()](mdn:js/Date/getUTCDay). `"get"`'ten sonra  `"UTC"` ekleyerek metodlara ulaşmak mümkündür.


Eğer bulunduğunuz saat dilimi `UTC+0` dan farklıysa `getHours()` ve `getUTCHours()` arasında bir farklılık olacaktır.

```js run
// o anki yerel tarih
let date = new Date();

// yerel saat
alert( date.getHours() );

// UTC+0'daki yerel saat( Londra kış saati)
alert( date.getUTCHours() );
```

Belirtilen metodlar dışında, UTC tipi olmayan iki tane özel metod bulunmaktadır:

[getTime()](mdn:js/Date/getTime)
: Verilen tarihin zaman damgasını ( timestamp ) döndürür -- 1 Ocak 1970 UTC+0'dan itibaren geçen milisaniye

[getTimezoneOffset()](mdn:js/Date/getTimezoneOffset)
: Yerel zaman ile UTC arasındaki farkı dakika olarak döndürür:

    ```js run
    // Eğer UTC-1'de yaşıyorsanız, çıktısı 60
    // Eğer UTC+3'de yaşıyorsanız, çıktısı -180
    alert( new Date().getTimezoneOffset() );

    ```

## Tarih bileşeninin ayarlama

Aşağıdaki metodlar tarih bileşenlerini ayarlamaya yarar:

- [`setFullYear(year, [month], [date])`](mdn:js/Date/setFullYear)
- [`setMonth(month, [date])`](mdn:js/Date/setMonth)
- [`setDate(date)`](mdn:js/Date/setDate)
- [`setHours(hour, [min], [sec], [ms])`](mdn:js/Date/setHours)
- [`setMinutes(min, [sec], [ms])`](mdn:js/Date/setMinutes)
- [`setSeconds(sec, [ms])`](mdn:js/Date/setSeconds)
- [`setMilliseconds(ms)`](mdn:js/Date/setMilliseconds)
- [`setTime(milliseconds)`](mdn:js/Date/setTime) (sets the whole date by milliseconds since 01.01.1970 UTC)

`setTime()` haricinde hepsinin `UTC` tipi de vardır, örneğin: `setUTCHours()`

Gördüğünüz gibi,`setHours` gibi bazı metodlar birden fazla bileşeni aynı anda ayarlamaya yarar. Bahsi geçmeyen bileşenlerde bir değişiklik yapılmaz.

Örneğin:

```js run
let bugun = new Date();

bugun.setHours(0);
alert(bugun); // bu gün ve saat 0

bugun.setHours(0, 0, 0, 0);
alert(today); // bu gün ve saniye 00:00:00.
```

## Otomatik Düzenleme

*Otomatik düzenleme* `Date` objesinin oldukça kullanışlı bir özelliğidir. Tarihi sınırın dışında ayarladığınız durumlarda otomatik olarak kendini düzeltebilir.

Örneğin:

```js run
let tarih = new Date(2013, 0, *!*32*/!*); // 32 Ocak 2013 ?!?
alert(tarih); // ...is 1st Şubat 2013!
```
Sınırın dışındaki tarih bileşenleri otomatik olarak dağıtılır.
Ayların sınırlarını düşünmenize gerek yoktur. Bunlar `Date` objesi tarafından otomatik olarak hesaplanacaktır.

Diyelim ki "28 Şub 2016"'yı iki gün artırmak istediniz. Belki "2 Mart" belki de "1 Mart" olabilir. Bunu bizim düşünmemize gerek yoktur. Sadece iki gün ekleyin yeterli. `Date` objesi geri kalanı sizin için yapacaktır:

```js run
let tarih = new Date(2016, 1, 28);
*!*
tarih.setDate(date.getDate() + 2);
*/!*

alert( tarih ); // 1 Mar 2016
```

Bu özellik belirtilen bir süre sonrasında tekrardan tarihi almak için kullanılır. Örneğin "Şu andan 70 sn sonrası"'ni al.

```js run
let tarih = new Date();
tarih.setSeconds(tarih.getSeconds() + 70);

alert( date ); // doğru tarihi gösterir.
```
Sıfır veya negatif değer de ayarlamak mümkündür. Örneğin:


```js run
let tarih = new Date(2016, 0, 2); // 2 Ocak 2016

tarih.setDate(1); // ayın 1. günü
alert( tarih );

tarih.setDate(0); // İlk gün 1 olduğundan dolayı 0 geçen ayın son gününü verir. min day is 1, so the last day of the previous month is assumed
alert( date ); // 31 Aralık 2015
```

## Tarihten sayıya, tarih farklılığı

`Date` objesi sayıya çevrildiğinde, aynı timestamp'te olduğu gibi `date.getTime()` değerini alır:

```js run
let tarih = new Date();
alert(+tarih); // date.getTime() ile aynı şekilde milisaniye döner.
```

Önemli not: tarihler birbirinden çıkarılabilir fakat sonuç ms cinsinden olur.

Bu iki tarih arasındaki zamanı ölçmek için kullanılabilir:

```js run
<<<<<<< HEAD:1-js/05-data-types/10-date/article.md
let baslangic = new Date(); // saymaya başla!
=======
let start = new Date(); // start measuring time
>>>>>>> 4d654318ccb6d37d6cefc9b859cf111ff3c96b27:1-js/05-data-types/11-date/article.md

// işi yap
for (let i = 0; i < 100000; i++) {
  let doSomething = i * i * i;
}

<<<<<<< HEAD:1-js/05-data-types/10-date/article.md
let bitis = new Date(); // bitt
=======
let end = new Date(); // end measuring time
>>>>>>> 4d654318ccb6d37d6cefc9b859cf111ff3c96b27:1-js/05-data-types/11-date/article.md

alert( `Döngü ${bitis - baslangic} ms` );
```

## Date.now()

<<<<<<< HEAD:1-js/05-data-types/10-date/article.md
Eğer sadece zaman farkını ölçmek istiyorsanız, `Date` objesine ihtiyacınız yok.
=======
If we only want to measure time, we don't need the `Date` object.
>>>>>>> 4d654318ccb6d37d6cefc9b859cf111ff3c96b27:1-js/05-data-types/11-date/article.md

Bunun için `Date.now()` adında bir obje bulunmakta.

Mantık olarak `new Date().getTime()` ile aynı olmasına rağmen yeni bir `Date` objesi oluşturmamaktadır. Bundan dolayı çok hızlı ve garbage collection'a yük bindirmemiş olur.

Genelde kullanışlı olduğundan veya performans özel JavaScript oyunları gibi uygulamalarda kullanılır.

Aşağıdaki daha iyidir denebilir:

```js run
*!*
let baslangic = Date.now(); // 1 Ocak 1970'den şimdiye kadar olan zamanın ms cinsinden değeri
*/!*

// işi yap
for (let i = 0; i < 100000; i++) {
  let doSomething = i * i * i;
}

*!*
let bitis = Date.now(); // done
*/!*

alert( `Döngü ${bitis - baslangic} ms sürdür` ); // sadece sayılar çıkarıldı tarihler değil.
```

## Kıyaslama

Eğer çok ağır yüklü işlemler için kıyaslama yapılıyorsa, dikkatli olunmalıdır.

Örneğin, iki tarih arasındaki farkı hesaplayan iki fonksiyondan hangisinin daha hızlı olduğunu inceleyelim

Such performance measurements are often called "benchmarks".

```js
// tarih1 ve tarih2, hangisi işlemi daha hızlı tamamlar.
function cikarma(tarih1, tarih2) {
  return tarih2 - tarih1;
}

// veya
function tarihFarki(tarih1, tarih2) {
  return tarih2.getTime() - tarih1.getTime();
}
```
Yukarıdaki iki fonksiyon aynı işlemi yapar, fakat bir tanesi `date.getTime()` ile o tarihin ms cinsinden değerini alırken diğeri tarihin sayıya doğrudan çevrilmesine dayalı. Sonuçları her zaman aynı olacaktır.

Öyleyse hangisi daha hızlı?

<<<<<<< HEAD:1-js/05-data-types/10-date/article.md
Bunu ölçmek için fonksiyonları birçok defa çalıştırıp aradaki farkı öyle kontrol etmektir.
=======
The first idea may be to run them many times in a row and measure the time difference. For our case, functions are very simple, so we have to do it at least 100000 times.
>>>>>>> 4d654318ccb6d37d6cefc9b859cf111ff3c96b27:1-js/05-data-types/11-date/article.md

Ölçülecek olursa:

```js run
function cikarma(tarih1, tarih2) {
  return tarih2 - tarih1;
}

function tarihFarki(tarih1, tarih2) {
  return tarih2.getTime() - tarih1.getTime();
}

function karsilastirma(f) {
  let tarih1 = new Date(0);
  let tarih2 = new Date();

  let baslangic = Date.now();
  for (let i = 0; i < 100000; i++) f(tarih1, tarih2);
  return Date.now() - baslangic;
}

alert( 'Çıkarma işlemi ile: ' + karsilastirma(cikarma) + 'ms' );
alert( 'tarihFarki islemi ile: ' + karsilastirma(tarihFarki) + 'ms' );
```

`getTime()` ile yapılan işlem çok daha hızlı! Bunun nedeni tip dönüşümü olmaması, böylece JavaScript motoru çok daha iyi optimize edebilmektedir.

Bir değer aldık fakat bu henüz iyi bir karşılaştırma olmadı.

<<<<<<< HEAD:1-js/05-data-types/10-date/article.md
Diyelim ki`karsilastirma(cikarma)` çalışırken işlemci paralelde başka birşeyler ile uğraşıyor olsun. Bu uğraştığı işlemler `karsilastirma(tarihFarki)` zamanında bitsin.

Bu aslında oldukça gerçekçi bir senaryodur.
=======
Imagine that at the time of running `bench(diffSubtract)` CPU was doing something in parallel, and it was taking resources. And by the time of running `bench(diffGetTime)` that work has finished.
>>>>>>> 4d654318ccb6d37d6cefc9b859cf111ff3c96b27:1-js/05-data-types/11-date/article.md

A pretty real scenario for a modern multi-process OS.

Sonuç olarak `karsilastirm(cikarma)` için daha az işlemci kaynağı kullanılanılır ve bu da yanlış sonuca neden olur.

**Daha güvenilir karşılaştırma yapabilmek için bu karşılaştırma paketi bir kaç defa çalıştırılmalıdır**

<<<<<<< HEAD:1-js/05-data-types/10-date/article.md
Aşağıda örneğini görebilirsiniz:
=======
For example, like this:
>>>>>>> 4d654318ccb6d37d6cefc9b859cf111ff3c96b27:1-js/05-data-types/11-date/article.md

```js run
function cikarma(tarih1, tarih2) {
  return tarih2 - tarih1;
}

function tarihFarki(tarih1, tarih2) {
  return tarih2.getTime() - tarih1.getTime();
}

function karsilastirma(f) {
  let tarih1 = new Date(0);
  let tarih2 = new Date();

  let baslangic = Date.now();
  for (let i = 0; i < 100000; i++) f(tarih1, tarih2);
  return Date.now() - baslangic;
}

let zaman1 = 0;
let zaman2 = 0;

*!*
// Paketi 10 defa çalışacak şekilde ayarlayın
for (let i = 0; i < 10; i++) {
  zaman1 += karsilastirma(cikarma);
  zaman2 += karsilastirma(tarihFarki);
}
*/!*

alert( 'Cikarma islemi ile geçen süre: ' + zaman1 );
alert( 'TarihFarki islemi ile geçen süre: ' + zaman2 );
```
Modern JavaScript motorları "sıcak kod" için daha gelişmiş optimizasyon yapmaya başladılar. Bu nadiren çalışan kodlar yerine daha çok fazlaca tekrar eden kodların optimizasyonu anlamına gelmektedir. Böylece ilk çalışmalar çok ta optimize edilmezler. 

```js
// ana döngüye girmeden ısınma turu:
karsilastirma(cikarma);
karsilastirma(tarihFarki);

// şimdi ise karşılaştırma ( benchmark )
for (let i = 0; i < 10; i++) {
  zaman1 += karsilastirma(cikarma);
  zaman2 += karsilastirma(tarihFarki);
}
```

<<<<<<< HEAD:1-js/05-data-types/10-date/article.md
```warn header="Mikro seviyede karşılaştırma yaparken daha dikkatli olunmalıdır."
=======
```warn header="Be careful doing microbenchmarking"
Modern JavaScript engines perform many optimizations. They may tweak results of "artificial tests" compared to "normal usage", especially when we benchmark something very small, such as how an operator works, or a built-in function. So if you seriously want to understand performance, then please study how the JavaScript engine works. And then you probably won't need microbenchmarks at all.
>>>>>>> 4d654318ccb6d37d6cefc9b859cf111ff3c96b27:1-js/05-data-types/11-date/article.md

Modern JavaScript motorları kod üzerinde birçok iyileştirme yaparlar. Normal kullanımdan ziyade yapay test sonuçları üzerinde değişikliklere neden olabilirler. Özellikle çok küçük karşılaştırmalarda. Bundan dolayı eğer performan sizin için çok ciddi bir konu ise, JavaScript motorlarının nasıl çalıştığını öğrenmeniz gerekmektedir. Öğrendiğinizde mikro seviyede bir karşılaştırmaya ihtiyacınız kalmayacaktır.

V8 motoru ile ilgili makaleleri <http://mrale.ph> adresinden bulabilirsiniz.
```

## Karakter dizisinden Date.parse ile tarih alma.

[Date.parse(str)](mdn:js/Date/parse) metodu karakterden tarih ayrıştırmaya yarar.

Metin formatı: `YYYY-MM-DDTHH:mm:ss.sssZ` şeklindedir, burada :

- `YYYY-MM-DD` -- tarih : yıl-ay-gün
- `"T"` karakteri ayraç.
- `HH:mm:ss.sss` -- zaman: saat:dakika:saniye.sarise şeklindedir.
- İsteğe bağlı olarak eklenen `'Z'` `+-hh:mm` şeklinde UTC'ye göre zaman ayarlamaya yarar. Varsayılan `Z` değeri UTC+0 anlamına gelir.

Daha kısa `YYYY-MM-DD` veya `YYYY-MM` hatta `YYYY` gibi şeklinde bile olabilir.

`Date.parse(str)` çağrısı verilen formatta karakterleri alır ve timestamp( 1 Ocak 1970 UTC+0'dan itibaren geçen sarise ) olarak geri döner. Eğer format doğru değilse, `NaN` döner.

Örneğin:

```js run
let ms = Date.parse('2012-01-26T13:51:50.417-07:00');

alert(ms); // 1327611110417  (timestamp)
```
Zaman damgasından (timestamp) `new Date` objesi yaratılabilir.

```js run
let tarih = new Date( Date.parse('2012-01-26T13:51:50.417-07:00') );

alert(tarih);  
```

## Özet
- Tarih ve saat bilgisi JavaScript'te [Date](mdn:js/Date) objesiyle temsil edilir. Sadece tarih veya saadece saat bilgisiyle obje oluşturulamaz: `Date` objesi her zaman iki bilgiyi de taşır.
- Aylar 0'dan başlar. ( Evet, Ocak ayı 0. aydır)
- Haftanın günü `getDate()` de 0'dan başlar ( Pazar günü )
- `Date` objesi eğer belirttiğiniz tarih mevcut değilse bunu hesaplayabilir. Bu gün,saat,ay ekleme/çıkarmak için kullanışlı bir özelliktir.
- Tarihler çıkartılabilir, aradaki fark sarise olarak döndürülür. Bunun nedeni `Date` sayıya çevrildiğinde zaman damgası olur.
- O anki zaman damgasını( timestamp ) almak için `Date.now()` kullanabilirsiniz.

Diğer sistemlerin aksine, zaman damgası javascripte saniye değil sarise cinsindendir.

<<<<<<< HEAD:1-js/05-data-types/10-date/article.md
Eğer daha ayrıntılı zaman bilgisine erişmek istiyorsanız. JavaScript desteklemese bile çoğu sistem microsaniyeye destek verir ( saniyenin milyonda biri ). Örneğin [performance.now()](mdn:api/Performance/now) sayfanın yüklenme süresini mikrosaniye cinsinden verir.
=======
Note that unlike many other systems, timestamps in JavaScript are in milliseconds, not in seconds.

Sometimes we need more precise time measurements. JavaScript itself does not have a way to measure time in microseconds (1 millionth of a second), but most environments provide it. For instance, browser has [performance.now()](mdn:api/Performance/now) that gives the number of milliseconds from the start of page loading with microsecond precision (3 digits after the point):
>>>>>>> 4d654318ccb6d37d6cefc9b859cf111ff3c96b27:1-js/05-data-types/11-date/article.md

```js run
alert(`Yüklemeye 4731.26000000001ms önce başladı`);
// Sonuç : Yüklemeye 4731.26000000001ms önce başladı
// .26 mikrosaniye (260 mikrosaniye)
// noktanın 3. basamağından sonraki değerler sapmadır fakat ilk 3 basamak doğrudur.
```
<<<<<<< HEAD:1-js/05-data-types/10-date/article.md
Node.JS `microtime` modülüne sahiptir. Teknik olarak her cihaz daha hassas tarih bilgisine ulaşabilir, sadece `Date` objesinde bu bilgiler yer almaz.
=======

Node.js has `microtime` module and other ways. Technically, almost any device and environment allows to get more precision, it's just not in `Date`.
>>>>>>> 4d654318ccb6d37d6cefc9b859cf111ff3c96b27:1-js/05-data-types/11-date/article.md