### Niğde | Aydın İş Kapısı 🏢✨

> “İş arayan ile işverenin aynı masaya oturduğu, kafa karıştırmayan, hızlı ve güvenli bir başvuru akışı.”

Ben bu projeyi Niğde odaklı, sade ama sağlam bir iş başvurusu platformu olarak kurguladım; amacım “ilan yayınla → doğru adayı bul → başvuruyu yönet” hattını gereksiz ekran kalabalığına boğmadan, temiz bir akış ve net sorumluluklar ile yürütmekti. 🌿  
Bu repo; hem kendi geliştirme disiplinimi (migrations, validation, security, katman ayrımı) gösterebildiğim, hem de gerçek hayatta ihtiyaç duyulan küçük ama kritik detayları (CV yükleme/indirme, şehir aramada autocomplete, yetki kontrolü gibi) işin merkezine koyduğum bir çalışma. 🧭

#### Proje neyi amaçlıyor? 🎯
Bu proje; “ilan paylaşmak isteyen işveren” ile “başvurmak isteyen aday” arasındaki iletişimi tek bir yerde, tek bir standartta toplar ve özellikle yerel ölçekte (Niğde) dağınık ilan/başvuru süreçlerini daha düzenli ve izlenebilir hale getirir. 🧩  
İşveren tarafı, ilanı hızlıca yayınlayıp gelen başvuruları tek ekranda görür; böylece “hangi ilana kim başvurdu, CV var mı, indirmek mümkün mü” gibi sorular tek bir tablo üzerinden cevaplanır. 📬  
Aday tarafı, ilanları listeden izleyip tek tıkla başvuru yapar; ayrıca CV ve profil bilgilerini güncelleyerek “başvurunun yanında eksik evrak kalmasın” mantığını korur. 🧑‍💻  
Arama tarafı, şehir bazlı autocomplete ile “yazdıkça öner, seçince ara” yaklaşımıyla kullanıcıyı yormaz; arama davranışını gereksiz filtre denizine çevirmeden hedefe götürür. 🔎

#### Hangi sorunlara çözüm getiriyor? 🛠️
Bu projeyi yazarken “küçük platform” gibi görünse de aslında sahada sürekli karşımıza çıkan dertleri hedefledim; yani süs olsun diye değil, gerçek akışta can yakan yerleri kapatmak için tasarladım.  
Dağınık başvuru takibi sorununu çözüyor; çünkü başvurular tek bir veri modeliyle kaydediliyor, işveren kendi ilanlarına gelen başvuruları sadece kendisi görebiliyor ve her satırda CV var mı yok mu net görünüyor. ✅  
Güvenlik ve yetki karmaşası yaşamıyorsun; çünkü candidate ve employer rollerini ayrı login sayfaları ve ayrı güvenlik zincirleriyle ayırdım, böylece “yanlış kullanıcı yanlış yere girdi” durumu pratikte önleniyor. 🔐  
Veritabanı disiplinini koruyor; çünkü Hibernate’in kafasına göre tablo üretmesine izin vermedim, ddl-auto=validate ile sadece doğrulatıp gerçek değişimi Flyway migration’lara emanet ettim, böylece şema kontrolü benim elimde kalıyor. 🧱  
Kullanıcı deneyimini hızlandırıyor; çünkü şehir önerisi input yazarken geliyor, kullanıcı “tam şehri yazayım, sonra arayayım” diye beklemiyor; küçük bir detay gibi ama arama hissini bambaşka yapıyor. ⚡

### Kullanılan teknolojiler (pom.xml üzerinden) 🧰
Bu proje Maven tabanlı; Java tarafında “az ama öz, iş yapan bağımlılık” yaklaşımını korudum ve proje büyüse bile sürdürülebilir kalacak bir temel kurdum.  
Teknoloji / Starter Ne işe yarıyor? (benim projede kullandığım anlamıyla)

| Teknoloji / Starter | Ne işe yarıyor? (benim projede kullandığım anlamıyla) |
|---|---|
| Java 21 ☕️ | Modern dil özelliklerini ve güncel JVM’i kullanarak daha uzun ömürlü bir altyapı hedefledim; özellikle Spring Boot 3.x dünyasında Java 21 rahat ve temiz bir çizgi veriyor. |
| Spring Boot 3.2.5 🚀 | Uygulamanın ayağa kalkması, konfigürasyonun sadeleşmesi, bağımlılıkların tutarlı yönetilmesi gibi işleri “framework ile kavga etmeden” çözmek için ana iskeletim. |
| spring-boot-starter-web 🌐 | MVC + Controller + Routing tarafını hızlı ve stabil kurmak için; hem HTML dönen sayfaları hem de JSON dönen autocomplete endpoint’ini aynı yerde rahatça yönetiyorum. |
| spring-boot-starter-thymeleaf 🧩 | Sunucu tarafı render (SSR) ile hızlı sayfa üretmek için; özellikle form binding (th:object, th:field) ve layout kompozisyonu bu projede kilit. |
| spring-boot-starter-security 🔐 | Candidate/Employer ayrımını rol bazlı oturtmak, login sayfalarını kontrol etmek, CV indir gibi hassas noktalarda yetkiyi sıkı tutmak için. |
| spring-boot-starter-validation ✅ | Formlarda “boş geçme, maksimum uzunluk, minimum karakter” gibi kuralları UI’da düzgün göstermek ve kullanıcıyı doğru yönlendirmek için. |
| spring-boot-starter-data-jpa 🗄️ | Kalıcı veriyi yönetmek için; repository katmanı ile query ihtiyaçlarını kontrollü ve okunur biçimde çözmek için. |
| Flyway (flyway-core) 🧱 | Şema değişikliklerini sürümleyip takip etmek için; “kimin makinesinde hangi tablo var” kaosunu bitiren şey burada Flyway. |
| H2 (runtime) 🧪 | Dev profilinde hızlı kalkış ve hızlı test için; aynı zamanda H2’yi PostgreSQL modunda çalıştırarak gerçek veritabanı davranışına yakın kalmaya çalıştım. |
| PostgreSQL (runtime) 🐘 | Prod profilinin ana veritabanı; gerçek hayatta taşınabilir, güçlü ve güvenilir. |
| spring-boot-starter-data-elasticsearch 🧲 | Şehir önerisi ve arama tarafında “ister DB, ister ES” diye büyüme yolu bırakmak için; şu an DB provider default, ES için skeleton hazır. |

Not: UI tarafında Bootstrap 5.3.3’ü CDN üzerinden kullanıyorum; buna ek olarak kendi “glass/dark” temam ile kart, form ve tablo görünümünü tek bir çizgide topladım. 🎨

### Mimari: Onion Architecture nedir, ne değildir? 🧅
Ben Onion Architecture’ı “proje klasörlerini dört parçaya bölüp havalı dursun” diye seçmedim; ben bunu işin özünü (domain + use-case mantığını) teknoloji heveslerinden ayırıp uzun ömürlü tutmak için seçtim, çünkü UI değişir, DB değişir, arama motoru değişir ama işin kuralı (kimin hangi ilana başvurabileceği, kimin hangi CV’yi indirebileceği, hangi verinin hangi yetkiyle görüleceği) değiştiğinde zaten iş değişmiş olur. 🧠🧱  
Benim hedefim şu: “Frameworkler projeyi yönetmesin; proje frameworkü kullansın.” Yani Spring, JPA, Thymeleaf burada patron değil, işi taşıyan araç. 🛠️

#### Onion Architecture nedir? ✅
Onion Architecture, “bağımlılıklar içeri doğru akar” kuralını saplantı gibi koruyan bir yaklaşım; yani dış dünya detayları (Spring MVC, Thymeleaf, JPA, Elasticsearch, dosya sistemi) içteki iş kurallarına asla hükmetmez, tam tersine dış katmanlar iç katmanların tarif ettiği arayüzlere uyum sağlayarak çalışır ve ben de bu sayede “yarın UI’yı değiştirsem bile” domain/use-case tarafını yerinden oynatmadan yoluma devam ederim. 🔄🧩  
Onion; domain’i merkeze koyar ve “iş kuralları zamanın dışında kalmalı” fikrini ciddiye alır; bu yüzden domain katmanında HTTP, JSON, Controller, EntityManager, annotation gibi kokular gezmez, çünkü o katman bir gün başka bir teknolojiyle de çalışabilecek kadar saf kalmalıdır. 🧬  
Onion, test edilebilirliği “sonradan eklenen bir lüks” değil, doğrudan tasarımın doğal sonucu yapar; çünkü application/use-case katmanı dış dünyayı interface/port üzerinden çağırdığı için ben, gerçek DB olmadan da “ilan kaydetme”, “başvuru oluşturma”, “CV erişim kontrolü” gibi kritik akışları rahatça test ederim. 🧪⚙️  
Onion’un asıl güzelliği bence şu: Kodun merkezinde sözleşmeler (port/interface) olur; altyapı katmanı bu sözleşmelere uyar, yani “veri nasıl saklanıyor” değişse bile “iş nasıl yürüyor” aynı kalır ve bu, büyüyen projelerde acayip bir huzur sağlar. 🤝✨

#### Onion Architecture ne değildir? ❌  
Onion Architecture “paketleri katmanlara ayırınca otomatik kalite gelir” demek değildir; eğer ben controller’dan repository’ye pat diye dalarsam, katman isimleri sadece makyaj olur, içeride yine aynı bağımlılık çorbası kaynar ve projenin borcu daha hızlı büyür. 🥣💣  
Onion Architecture “DDD’nin kendisi” değildir; DDD bir düşünme ve modelleme disiplinidir, Onion ise o modeli korumak için sınır çizmenize yardım eden mimari bir çerçevedir, yani DDD yapmadan da Onion yaparsın ama Onion yapınca “domain’i koruyacak bariyerler” daha kolay kurulur. 🧷  
Onion Architecture “her şeye ayrı klasör aç, her şeyi interface yap” fetişi değildir; ben interface’i sadece gerçekten sınır olan yerde kullanırım (DB, dosya, arama motoru gibi), yoksa gereksiz soyutlama hem okunabilirliği düşürür hem de geliştirme hızını baltalar. 🪓  
Onion Architecture mikroservis şartı değildir; tek uygulamada da çok işe yarar, çünkü konu mikroservis değil, konu “iş kuralları ile dış dünya detaylarının birbirini zehirlememesi”dir. 🧱

#### Bu projede katmanlar nasıl duruyor? 🗺️  
Domain (domain): Benim için burası “kavramların evi”; User, JobPost, Application gibi çekirdek anlamlar burada durur ve bu katmanda Spring annotation’ı, JPA entity detayı, HTTP request bilgisi gibi şeyler barındırmam; çünkü domain’in görevi teknolojiyle uğraşmak değil, işin doğru tanımını taşımaktır. 🧬📌  
Application (application): Burası “use-case dili”; yani sistemin ne yaptığını cümleye döken katman; “ilan yayınla”, “başvuru oluştur”, “başvuruları listele”, “CV indirilebilir mi?” gibi kararların aklı burada durur ve bu akıl, dış dünyaya sadece port/interface üzerinden seslenir. 🧠🔌  
Infrastructure (infrastructure): Burası dış dünyanın gerçekliği; JPA entity’leri, repository implementasyonları, dosya depolama, arama provider’ı gibi “nasıl yaptığımızın” tüm detayları burada; yani application “bana başvuruları getir” der, infrastructure “tamam, ben DB’den şöyle çekerim” diye işi gerçekleştirir. 🗄️🔧  
Presentation (presentation): Controller + form DTO + Thymeleaf sayfaları burada; yani kullanıcıyla konuşan yüz; burası hızlı değişir, tasarım değişir, ekran değişir, validation mesajı değişir ama ben iş kurallarını buraya gömmem, çünkü UI tarafı değiştiğinde işin özü de sürüklenmesin isterim. 🖥️🎨

#### Clean Architecture vs Onion Architecture farkı 🧼🧅  
İkisi de aynı büyük fikrin etrafında döner: Dependency Inversion (DIP) ve “çekirdeği koru” prensibi; ama ben aralarındaki farkı şöyle görüyorum: Onion daha çok domain merkezli bir soğan gibi hissedilirken, Clean Architecture daha “use-case merkezli” ve daha tarifli/kurallı bir daireler düzeni gibi çalışır. 🧠📐  
Onion, benim kafamda “domain’i kutsal tut, dış dünyayı dışarıda bırak” yaklaşımıdır; domain’in etrafında application servisleri ve en dışta infrastructure/presentation döner, yani merkezdeki anlamı korumak birinci önceliktir ve bu projede ben bunu özellikle kullanıcı-rol-yetki gibi konularda bilinçli yaptım. 🧅🛡️  
Clean Architecture, katmanları daha net isimlerle tarif eder: Entities → Use Cases → Interface Adapters → Frameworks & Drivers; yani “use-case” katmanı çok bariz bir şekilde merkeze oturur ve UI/DB gibi şeyler “driver” olarak en dışta kalır, bu da ekiplerde standardizasyonu artırır çünkü herkes aynı haritayı okur. 🧼🧭  
Pratikte ikisi de “dış katmanlar içe bağımlı olsun” der; fark çoğu zaman felsefede değil, terminolojide ve sınırların nasıl çizildiğinde çıkar: Clean Architecture genelde boundary/adapter ayrımını daha keskin vurgular, Onion ise domain etrafında dönen servis halkalarını daha doğal anlatır. 🔁  
Ben bu projede Onion çizgisini seçerken aslında Clean Architecture’ın “use-case odaklı” disiplinini de içeri taşımaya çalıştım; yani controller’ların içinde iş kuralı büyütmek yerine, akışı application tarafında toparlayıp presentation’ı daha çok “input/output taşıyan yüz” olarak bıraktım, böylece UI değişse bile use-case mantığı aynı kaldı. 🧠➡️🖥️  
Kısacası: Onion benim için “domain’i koruyan zırh”, Clean Architecture ise “use-case’i merkezde tutan pusula”; ben ikisini rakip değil, doğru uygulandığında birbirini besleyen iki yaklaşım olarak görüyorum, çünkü ikisinin de hedefi aynı: “kod büyürken kontrolü kaybetme.” 🛡️🧭  
Benim kırmızı çizgim: Hangi isimle çağırırsak çağıralım, iş kuralı UI’ya akmıyorsa, DB detayı use-case’i kirletmiyorsa, bağımlılık yönü içeri doğru korunuyorsa mimari görevini yapıyor demektir. ✅

#### Thymeleaf yapısı: ben nasıl kullanıyorum? 🍃  
Thymeleaf’i “HTML içine Java yazma(JSP)” gibi kullanmıyorum; tam tersine, HTML’i temiz tutup, binding ve koşullu render gibi işleri “gerektiği kadar” yapıyorum ki hem tasarım bozulmasın hem de backend verisi doğru yere otursun.  
Layout kompozisyonu: templates/layout.html içinde th:fragment="layout(content)" ile bir ana iskelet var; sayfalar da th:replace="layout :: layout(~{::section})" diyerek kendi <section> içeriğini layout’un içine oturtuyor, böylece navbar, stil, script gibi tekrarlar tek yerde kalıyor. 🧱  
Form binding: Form sayfalarında th:object="${form}" ve input’larda th:field="*{...}" kullanıyorum; bu sayede validation hataları #fields.hasErrors(...) ile doğrudan UI’ya taşınıyor ve kullanıcı “neden olmadı?” diye boş boş bakmıyor. ✅  
Template düzeni: auth/, candidate/, employer/, search/, error/ diye ayrılmış klasör yapısı var; bu ayrım bana hem okunabilirlik hem de “hangi ekran nereye ait?” netliği veriyor. 🧭

#### Veritabanı + Migration disiplini (Flyway) 🗃️🧱  
Ben “proje çalışsın” diye veritabanını framework’e bırakmayı sevmiyorum; çünkü gerçek hayatta en ufak şema kayması, prod’da acıtır, bu yüzden şemayı migration ile yönetmek benim için bilinçli bir tercih.  
spring.jpa.hibernate.ddl-auto=validate kullanıyorum; bu ayar “Hibernate tablo üretsin” değil, “mevcut şema ile entity’ler uyumlu mu kontrol et” demek, yani migration dışı bir sapma olursa uygulama daha baştan uyarı veriyor. 🚦  
Flyway migration dosyaları src/main/resources/db/migration altında; burada “kimin ne zaman ne eklediği” net, geri dönüşü ve izlenebilirliği var. 🧾

#### Şema özeti (tablo isimleri ve niyeti) 🧩  
Tablo Bu tabloda ne var, bu proje açısından niye önemli?

| Tablo | Bu tabloda ne var, bu proje açısından niye önemli? |
|---|---|
| users 👤 | Kullanıcı kimliği, email, şifre hash’i ve rol bilgisi burada; bu tablo “candidate mi employer mı” ayrımının temeli ve her şeyin bağlandığı kök nokta. |
| candidate_profile 🧑‍💻 | Adayın CV’ye dair bilgileri (iş geçmişi, deneyim yılı, askerlik, okul, CV dosya yolu gibi) burada; başvurunun niteliğini artıran şey aslında bu profil. |
| employer_profile 🏢 | İşverenin firma adı ve logo gibi bilgileri burada; ilanların arkasında kurumsal bir “kimlik” olsun diye duruyor. |
| job_post 📢 | İlanın başlık/şehir/detay bilgisi ve ilanı açan employer id burada; yani “işverenin vitrini” bu tablo. |
| job_application 📬 | Adayın hangi ilana başvurduğu, başvuru zamanı ve durum bilgisi burada; ayrıca aynı ilana aynı adayın tekrar tekrar başvurmasını engelleyen unique constraint mantığı burada korunuyor. |

#### Çalıştırma (dev / prod) 🚀  
Gereksinimler: Java 21, Maven, (prod için) PostgreSQL

#### Dev (H2 ile hızlı kalkış) 🧪
```bash
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```
Dev profilinde H2 kullanıyorum; hızlı ayağa kalkar, Flyway migration’lar uygulanır ve UI anında ayağa kalkar. ⚡  
H2 Console açıktır (geliştirme rahatlığı için); ama prod’da bu yaklaşımı kullanmıyorum, çünkü güvenlik açısından doğru yer orası değil. 🛡️

#### Prod (PostgreSQL ile) 🐘
```bash
mvn spring-boot:run -Dspring-boot.run.profiles=prod
```
Prod profilinde application-prod.yml içindeki PostgreSQL bağlantısı devreye girer; Flyway migration’lar yine kontrollü biçimde çalışır ve şema tutarlılığı korunur. 🧱

#### Sayfa / Endpoint haritası 🧭  
Aşağıdaki rotaları özellikle net tuttum; çünkü bir projeyi büyüten şey “kaç endpoint var” değil, “kullanıcının zihninde yol haritası var mı” meselesi.  
Rota Kim kullanır? Ne yapar, neden var?

| Rota | Kim kullanır? | Ne yapar, neden var? |
|---|---|---|
| / 🏠 | Herkes | HTML olarak ana sayfayı döner; ayrıca farklı produces ile sade bir “OK” health cevabı da vererek ortam kontrolünü kolaylaştırır. |
| /login/candidate 🔑 | Candidate | Aday giriş ekranı; candidate rolünü ayrı bir login akışıyla tutarak karışıklığı azaltır. |
| /login/employer 🔑 | Employer | İşveren giriş ekranı; işveren tarafındaki yetkili sayfalara giden kapı burası. |
| /register/candidate ✍️ | Candidate | Aday kayıt ekranı; email uniqueness ve validation ile “kayıt süreci düzgün kapanıyor mu” konusu burada kontrol altında. |
| /register/employer ✍️ | Employer | İşveren kayıt ekranı; employer profile tarafının temeli burada atılıyor. |
| /candidate/jobs 🧑‍💻 | Candidate | İlan listesi; aday burada ilanlara bakar ve başvuru aksiyonunu başlatır. |
| /candidate/jobs/{jobId}/apply ✅ | Candidate | Aday başvurusu; aynı ilana ikinci kez başvuruyu engelleyen kontrol burada. |
| /candidate/cv 📄 | Candidate | CV/profil düzenleme; dosya yükleme sınırları ve depolama mantığı burada çalışır. |
| /employer/job-posts/new 📢 | Employer | İlan oluşturma ekranı; başlık/şehir/detay validasyonu ile ilan kalitesini korur. |
| /employer/job-posts 💾 | Employer | İlan kaydetme; employer id ile ilişkilendirerek “ilanın sahibi kim” bilgisini sağlam tutar. |
| /employer/applications 📬 | Employer | Başvuru listesi; işveren kendi ilanlarına gelen başvuruları görür, aday email/status ve CV durumunu burada izler. |
| /employer/applications/{applicationId}/cv ⬇️ | Employer | CV indirme; sadece ilgili ilanın sahibi olan employer indirebilir, yani yetki kontrolü bu endpoint’te sıkı durur. |
| /search 🔎 | Herkes | Şehir bazlı arama; seçilen şehirdeki ilanları listeler. |
| /search/suggest?city=... ✨ | Herkes | Autocomplete JSON; input yazdıkça şehir önerisi verir, kullanıcı deneyimini hızlandırır. |

#### Kod haritası (özetle “nerede ne var?”) 🗺️  
Ben bu projede isimlendirmeyi özellikle açık tuttum; dosyaya bakan kişi “bu sınıf ne iş yapıyor?” diye düşünmeden yolunu bulabilsin istedim.
```text
src/main/java/com/example/jobplatform
├─ domain
│  └─ user/User.java                       -> Çekirdek kullanıcı modeli (framework bağımsız)
├─ application
│  ├─ user/UserService.java                -> Kullanıcı use-case arayüzü
│  ├─ user/CreateUserCommand.java          -> Kayıt komutu (input’ları taşır)
│  └─ search/JobSearchService.java         -> Arama use-case arayüzü
├─ infrastructure
│  ├─ persistence/jpa/*                    -> JPA entity + repository katmanı (DB detayları)
│  ├─ persistence/adapter/UserServiceImpl  -> Application arayüzünün DB ile çalışan implementasyonu
│  ├─ storage/CvStorage.java               -> CV dosyalarını güvenli şekilde diske yazma
│  └─ search/DbJobSearchService.java       -> Varsayılan arama provider’ı (DB üzerinden)
└─ presentation
   ├─ config/SecurityConfig.java           -> Candidate/Employer zincirleriyle güvenlik kurgusu
   └─ web/*                                -> Controller’lar + form DTO’lar (UI kapısı)
```

#### Koddan minik ama anlamlı kesitler 📌  
Aşağıdaki parçalar benim için “projenin omurgası” gibi; kısa görünüyor ama sistemin davranışını belirleyen yerler buralar.

#### 1) Şehir autocomplete endpoint’i (SearchController) 🔎✨
```java
@GetMapping(value = "/suggest", produces = MediaType.APPLICATION_JSON_VALUE)
@ResponseBody
public List<String> suggest(@RequestParam(name = "city") String city) {
    return jobSearchService.suggestCities(city);
}
```

#### 2) Migration disiplininin kalbi (application.yml) 🧱
```yml
spring:
  jpa:
    hibernate:
      ddl-auto: validate
  flyway:
    enabled: true
```

#### 3) Employer CV indirmede yetki kontrolü 🔐⬇️
```java
JobPostJpaEntity post = jobPostRepository.findById(app.getJobPostId()).orElse(null);
if (post == null || !Objects.equals(post.getEmployerId(), employerId)) {
    return ResponseEntity.status(HttpStatus.FORBIDDEN).build();
}
```

#### Küçük notlar (tasarım & UX) 🎨  
Bu projede “Bootstrap giydirip bırakmak” yerine, koyu temalı glass bir hissiyat hedefledim; özellikle kartlar, form alanları ve tablolar aynı karakterde dursun diye layout içinde merkezi bir stil yönetimi yaptım. 🌙  
Ayrıca static/js/autocomplete.js ile input yazdıkça öneri gösteren ufak bir JS akışı var; bu kısım benim gözümde “küçük ama etkisi büyük” detaylardan biri. ⚡

#### Yol haritası (bir sonraki adımda ne yaparım?) 🧠🛣️  
Elasticsearch’i gerçekten devreye alıp şehir önerisini ve aramayı “scale” edilebilir hale getiririm; ama bunu yaparken de app.search.provider yaklaşımını korur, provider değişimini konfigürasyona bağlarım ki kod değil ayar konuşsun. 🧲  
Başvuru durumlarını (APPLIED → REVIEWED → REJECTED/ACCEPTED) gibi bir state makinesine çevirip employer panelinde yönetilebilir hale getiririm; çünkü gerçek hayatta asıl değer “başvuruyu aldım” değil, “başvuruyu yönettim” kısmında. 📌  
Dosya depolamayı local disk yerine S3 benzeri bir çözüme taşırım; ama yine CvStorage gibi bir sınır bırakırım ki altyapı değişse de application/presentation tarafı sarsılmasın. ☁️  
UI tarafında küçük erişilebilirlik dokunuşları (kontrast, odak halkası, klavye navigasyonu) eklerim; çünkü hızlı sistem kadar “rahat kullanılan” sistem de önemlidir.


#### Görseller:

<img width="1919" height="448" alt="Screenshot_17" src="https://github.com/user-attachments/assets/38b7f224-24e8-4abb-ab07-f1d102b3b8d6" />
<img width="1919" height="1079" alt="Screenshot_16" src="https://github.com/user-attachments/assets/d5ab1ac2-5d9a-4043-8901-03083201484e" />
<img width="1919" height="1079" alt="Screenshot_15" src="https://github.com/user-attachments/assets/351c94a9-6405-4266-86c3-a6f3458d18a4" />
<img width="1919" height="1079" alt="Screenshot_14" src="https://github.com/user-attachments/assets/619a9492-ba19-4c55-9c25-eb42c4e76d24" />
<img width="1919" height="1079" alt="Screenshot_13" src="https://github.com/user-attachments/assets/8beda9cb-5399-4f0e-9f69-ad6685888e90" />
<img width="1919" height="1079" alt="Screenshot_12" src="https://github.com/user-attachments/assets/dbd9ef0a-ad38-4a3a-b15e-e8e51587e778" />
<img width="1919" height="1079" alt="Screenshot_11" src="https://github.com/user-attachments/assets/6e671090-3bfa-4452-be47-1f54b48339db" />
<img width="1919" height="1079" alt="Screenshot_10" src="https://github.com/user-attachments/assets/9d7ab5aa-f7f2-456d-aff2-9107e6bb0983" />
<img width="1919" height="1079" alt="Screenshot_9" src="https://github.com/user-attachments/assets/0d89eef2-ebed-435c-a729-8d7c8a619d1c" />
<img width="1919" height="1079" alt="Screenshot_8" src="https://github.com/user-attachments/assets/16db4cb7-1ea1-4f2f-8279-561940717c19" />
<img width="1919" height="1079" alt="Screenshot_7" src="https://github.com/user-attachments/assets/8f67a53e-f369-47de-9111-f9197b7af5fd" />
<img width="1919" height="1079" alt="Screenshot_6" src="https://github.com/user-attachments/assets/9a5ab743-2dc9-4b17-ba8b-7e1e1f59b59b" />
<img width="1919" height="1079" alt="Screenshot_5" src="https://github.com/user-attachments/assets/35636448-ac4c-47fc-bdeb-e254ba974134" />
<img width="1919" height="1079" alt="Screenshot_4" src="https://github.com/user-attachments/assets/07cfa004-f9ea-47bc-b5d1-484b7371928b" />
<img width="1919" height="1079" alt="Screenshot_3" src="https://github.com/user-attachments/assets/b62c55d0-c704-4d4d-86ce-5c21d8b21da4" />
<img width="1919" height="1079" alt="Screenshot_2" src="https://github.com/user-attachments/assets/2a201b0a-b908-4797-87aa-2ea6b50d4043" />
<img width="1919" height="1079" alt="Screenshot_1" src="https://github.com/user-attachments/assets/04c950e2-2190-46bb-b5d6-c13e3ce430ad" />

