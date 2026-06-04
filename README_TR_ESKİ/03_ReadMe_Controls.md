# Step 3: Controls

https://sapui5.hana.ondemand.com/#/topic/ddbceecd7d3d42eea9cf78a820a238fb

## Genel Bakış
Bu adımda **Hello World** metnini HTML içine doğrudan yazmak yerine, SAPUI5’in **sap/m/Text** kontrolünü kullanarak ekrana yazdıracağız.  
Bu sayede SAPUI5’in **kontrol API’si** ile kullanıcı arayüzü oluşturmayı öğreniyoruz.

---

## Adım Adım

### 1️⃣ index.html Düzenleme
- `webapp/index.html` dosyasında `<body>` içindeki `<div>Hello World</div>` satırını silin.  
- `<body>` etiketine **class** ve **id** ekleyin:
  ```html
  <body class="sapUiBody" id="content">
  </body>
````

* `sapUiBody` sınıfı → Tema bazlı SAPUI5 stillerini uygular.
* `id="content"` → SAPUI5 kontrolümüzün yerleştirileceği DOM elemanı.

---

### 2️⃣ index.js Düzenleme

* `webapp/index.js` dosyasını aşağıdaki gibi düzenleyin:

  ```javascript
  sap.ui.define([
      "sap/m/Text"
  ], (Text) => {
      "use strict";

      new Text({
          text: "Hello World"
      }).placeAt("content");
  });
  ```
* Açıklama:

  * `"sap/m/Text"` → SAPUI5’in `sap.m` kütüphanesindeki **Text** kontrolünü yüklüyor.
  * `text: "Hello World"` → Kontrolün **text** özelliğini ayarlıyor.
  * `.placeAt("content")` → Kontrolü `id="content"` olan HTML elemanına yerleştiriyor.

---

## Kontrol Mantığı

* SAPUI5’te **kontroller**, ekranın görünümünü ve davranışını tanımlar.
* Tüm kontroller **sap.ui.core.Control** sınıfından türetilir.
* `placeAt()` metodu → Kontrolü doğrudan bir DOM elemanına veya başka bir kontrolün içine eklemek için kullanılır.
* Her kontrolün:

  * **Properties (özellikler)**
  * **Aggregations (alt öğeler)**
  * **Associations (ilişkilendirmeler)**
    bulunur. Ayrıntılar **Demo Kit**’te görülebilir.

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
3. Tarayıcıda `index.html` açıldığında **Hello World** yazısı artık SAPUI5 kontrolü ile görüntülenir.

---

## Klasör ve Dosya Yapısı

```
C:\sapui5\SAPUI5_TUTORIALS\hello_world
│   package.json
│   ui5.yaml
│
└───webapp
     │   index.html
     │   index.js
     │   manifest.json
```

---

## Notlar

* Artık HTML içine doğrudan metin yazmak yerine **kontroller** üzerinden içerik ekleyeceğiz.
* `sap/m/Text` sadece bir örnek, ilerleyen adımlarda farklı kontrolleri öğreneceğiz.

```

