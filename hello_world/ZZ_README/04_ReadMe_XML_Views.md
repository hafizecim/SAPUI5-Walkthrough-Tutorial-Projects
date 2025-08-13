# Step 4: XML Views

https://sapui5.hana.ondemand.com/#/topic/1409791afe4747319a3b23a1e2fc7064

## Genel Bakış
Bir önceki adımda (`Step 3`) tüm kullanıcı arayüzünü (**UI**) `index.js` içinde oluşturuyorduk.  
Bu yöntem, uygulama büyüdükçe karmaşıklaşır.  
Bu adımda, SAPUI5’in **XML View** yapısını kullanarak UI tanımını JavaScript’ten ayıracağız.

**Avantajlar:**
- Daha okunabilir kod
- Görünüm (View) ve mantık (Controller) ayrımı
- Modüler yapı

---

## Adım Adım

### 1️⃣ View Klasörü ve Dosya Oluşturma
- `webapp` içinde **view** adında yeni bir klasör oluşturun.
- Bu klasörün içine `App.view.xml` dosyası ekleyin.
- Başlangıç yapısı:
  ```xml
  <mvc:View
     xmlns="sap.m"
     xmlns:mvc="sap.ui.core.mvc">
  </mvc:View>
````

**Açıklama:**

* `xmlns="sap.m"` → Varsayılan namespace, SAPUI5’in çoğu UI kontrolü burada.
* `xmlns:mvc="sap.ui.core.mvc"` → MVC bileşenleri (View, Controller vb.) için namespace.
* `mvc:View` → XML View’in kök elemanı.

---

### 2️⃣ Text Kontrolünü XML’e Taşıma

* `App.view.xml` içine Text kontrolünü ekleyin:

  ```xml
  <mvc:View
     xmlns="sap.m"
     xmlns:mvc="sap.ui.core.mvc">
     <Text text="Hello World"/>
  </mvc:View>
  ```
* Buradaki `<Text>` etiketi `sap/m/Text` kontrolüne karşılık gelir.
* `text` özelliği XML’de **attribute** olarak tanımlanır.

---

### 3️⃣ index.js Güncelleme

* `webapp/index.js` dosyasını şu şekilde düzenleyin:

  ```javascript
  sap.ui.define([
      "sap/ui/core/mvc/XMLView"
  ], (XMLView) => {
      "use strict";

      XMLView.create({
          viewName: "ui5.walkthrough.view.App"
      }).then((oView) => oView.placeAt("content"));
  });
  ```

**Açıklama:**

* `"sap/ui/core/mvc/XMLView"` → XML tabanlı bir view oluşturmak için gerekli sınıf.
* `viewName` → View’in tam namespace yolu.

  * Burada `"ui5.walkthrough.view.App"` →

    * `ui5.walkthrough` namespace (manifest.json veya proje yapısına göre belirlenir)
    * `view` klasör adı
    * `App` dosya adı (`.view.xml` uzantısı eklenmez)
* `.placeAt("content")` → Oluşturulan view’i `id="content"` olan HTML elemanına yerleştirir.

---

## Konvansiyonlar

* View dosya isimleri **büyük harfle** başlar (örn. `App.view.xml`).
* Tüm view dosyaları **view** klasöründe saklanır.
* XML view dosyalarının uzantısı **.view\.xml**’dir.
* Varsayılan XML namespace → `sap.m`
* Diğer namespace’ler, SAP namespace’inin son kısmını alias olarak kullanır
  (ör. `sap.ui.core.mvc` → alias: `mvc`)

---

## Terminal Komutları

1. Proje klasörüne gidin:

   ```powershell
   cd C:\sapui5\SAPUI5_TUTORIALS\hello_world
   ```
2. UI5 sunucusunu başlatın:

   ```powershell
   npm start
   ```
3. Tarayıcıda uygulamayı açın → Görsel olarak Step 3 ile aynı olacak, ancak kod yapısı artık daha düzenli.

---

## Klasör Yapısı

```
C:\sapui5\SAPUI5_TUTORIALS\hello_world
│   package.json
│   ui5.yaml
│
└───webapp
     │   index.html
     │   index.js
     │   manifest.json
     │
     └───view
          │   App.view.xml
```

---

## Notlar

* Bu adımda **UI görünümü** ve **uygulama mantığı** ayrıldı.
* Kodun modüler hale gelmesi, ilerleyen adımlarda Controller, Model ve Event yönetimini kolaylaştırır.
* Görünümde (`App.view.xml`) değişiklik yapmadan, Controller ile UI mantığını değiştirebilirsiniz.

```


