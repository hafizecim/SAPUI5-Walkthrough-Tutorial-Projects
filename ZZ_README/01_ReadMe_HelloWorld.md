# SAPUI5 Walkthrough - Step 1: Hello World

https://sapui5.hana.ondemand.com/#/topic/2680aa9b16c14a00b01261d04babbb39

Bu adımda SAPUI5 projesinin temel yapısını kuruyor ve basit bir “Hello World” sayfası çalıştırıyoruz.

Dikkat terminali en sona bırakabilirsin!!!
---

## 1️⃣ UI5 CLI’yi Global Olarak Kurma
- Terminali açın ve `npm install --global @ui5/cli` komutunu çalıştırın.  
**Ne işe yarar?**  
SAPUI5 projelerini başlatmak, geliştirme sunucusunu açmak ve paketlemek için gerekli olan **UI5 Tooling** aracını bilgisayarınıza global olarak yükler.

---

## 2️⃣ Proje Ana Klasörünü Oluşturma
- Bilgisayarınızda bir klasör oluşturun ve buna **app root folder** adını verin. Bu proje için hello_world
**Ne işe yarar?**  
Bu klasör projenin tüm kaynak dosyalarını ve yapılandırma dosyalarını içerecek ana dizindir.

---

## 3️⃣ package.json Dosyası Oluşturma
- **app root folder** içinde `package.json` adında bir dosya oluşturun ve içerisine proje bilgilerini ekleyin.  
**Ne işe yarar?**  
Proje adı, sürüm bilgisi ve çalıştırma komutları gibi bilgileri tutar.  
Ayrıca `"start"` komutuyla geliştirme sunucusunu çalıştırmamıza imkan verir.

---

## 4️⃣ webapp Klasörünü Oluşturma
- **app root folder** içinde `webapp` adında bir klasör oluşturun.  
**Ne işe yarar?**  
Tarayıcıya yüklenecek tüm HTML, CSS, JavaScript dosyalarının saklandığı ana klasördür.

---

## 5️⃣ index.html Dosyası Oluşturma
- `webapp` klasörünün içine `index.html` adında bir dosya oluşturun.  
**Ne işe yarar?**  
Projenin ilk açılış sayfasıdır. Burada başlık ve “Hello World” gibi ilk içerikler yer alır.

---

## 6️⃣ manifest.json Dosyası Oluşturma
- `webapp` klasöründe `manifest.json` adında bir dosya oluşturun.  
**Ne işe yarar?**  
Uygulama tanımlayıcısıdır (**app descriptor**). Uygulamanın ID’si, sürüm bilgisi ve yapılandırma ayarlarını saklar.

---

## 7️⃣ Proje İçin UI5 CLI Bağımlılıklarını Kurma
- Terminalde **app root folder** içinde `npm i -D @ui5/cli` komutunu çalıştırın.  
**Ne işe yarar?**  
UI5 CLI aracını proje içine **geliştirme bağımlılığı** olarak ekler.
Bu kurulum ile gelen folder : node_modules
Bu kurulum ile gelen dosyalar: package-lock.json ve package.json

---

## 8️⃣ UI5 Projesini Başlatma
- Terminalde `ui5 init` komutunu çalıştırın. 
Oluşan dosya: ui5.yaml
**Ne işe yarar?**  
`ui5.yaml` dosyasını oluşturarak projenin UI5 yapılandırmasını başlatır.

---

## 9️⃣ Projeyi Çalıştırma
- Terminalde `npm start` komutunu çalıştırın. Tüm dosyaların kayıt olduğundan emin ol. 
**Ne işe yarar?**  
Geliştirme sunucusunu çalıştırır ve tarayıcıda `index.html` dosyasını açarak “Hello World” sayfasını görüntüler.

---

## 📌 Sonuç
Bu adım sonunda, SAPUI5 projesinin temel dosya yapısını oluşturmuş ve tarayıcıda çalışan ilk sayfamızı hazırlamış olduk.

