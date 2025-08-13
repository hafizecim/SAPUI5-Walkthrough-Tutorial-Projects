# Step 8: Translatable Texts (i18n)

https://sapui5.hana.ondemand.com/#/topic/df86bfbeab0645e5b764ffa488ed57dc

## Genel Bakış
Bu adımda, UI’daki sabit metinleri **i18n** (internationalization) yöntemiyle harici bir **resource file**’a taşıyacağız.  
Böylece:
- Tüm metinler tek bir yerde toplanır.
- Kolayca farklı dillere çevrilebilir.
- Uygulama çok dilli destek kazanır.

---

## 1️⃣ i18n Klasörü ve Dosyası Oluşturma

📂 `webapp/i18n/i18n.properties`  
İçerik:

```properties
showHelloButtonText=Say Hello
helloMsg=Hello {0}
````

### Açıklamalar:

* **Key = Value** formatı kullanılır.
* `{0}` → Dinamik parametre. Controller’dan veri ile doldurulur.
* Her dil için ayrı dosya kullanabilirsiniz:

  * `i18n.properties` → Varsayılan dil.
  * `i18n_en.properties` → İngilizce.
  * `i18n_de.properties` → Almanca.
* SAPUI5, tarayıcı dil ayarına göre uygun dosyayı yükler, bulamazsa varsayılanı kullanır.

---

## 2️⃣ Controller Güncelleme

📄 `webapp/controller/App.controller.js`

```javascript
sap.ui.define([
   "sap/ui/core/mvc/Controller",
   "sap/m/MessageToast",
   "sap/ui/model/json/JSONModel",
   "sap/ui/model/resource/ResourceModel"
], (Controller, MessageToast, JSONModel, ResourceModel) => {
   "use strict";

   return Controller.extend("ui5.walkthrough.controller.App", {
     onInit() {
         // JSON model (data)
         const oData = {
            recipient : {
               name : "World"
            }
         };
         const oModel = new JSONModel(oData);
         this.getView().setModel(oModel);

         // i18n model (texts)
         const i18nModel = new ResourceModel({
            bundleName: "ui5.walkthrough.i18n.i18n"
         });
         this.getView().setModel(i18nModel, "i18n");
      },

      onShowHello() {
         // i18n model’den metin al
         const oBundle = this.getView().getModel("i18n").getResourceBundle();
         const sRecipient = this.getView().getModel().getProperty("/recipient/name");
         const sMsg = oBundle.getText("helloMsg", [sRecipient]);

         // Mesaj göster
         MessageToast.show(sMsg);
      }
   });
});
```

### Açıklamalar:

* **`ResourceModel`**: i18n dosyalarına erişim için kullanılır.
* **`bundleName`**: `namespace.klasör.dosyaAdı` formatında olmalı (uzantı yazılmaz).
* **Named Model ("i18n")**: View içinde `i18n>` ile erişilir.
* **`getText("key", [param])`**: i18n metnindeki `{0}` vb. yerleri dinamik veri ile doldurur.

---

## 3️⃣ View Güncelleme

📄 `webapp/view/App.view.xml`

```xml
<mvc:View
   controllerName="ui5.walkthrough.controller.App"
   xmlns="sap.m"
   xmlns:mvc="sap.ui.core.mvc">

   <Button
      text="{i18n>showHelloButtonText}"
      press=".onShowHello"/>

   <Input
      value="{/recipient/name}"
      description="Hello {/recipient/name}"
      valueLiveUpdate="true"
      width="60%"/>
</mvc:View>
```

### Açıklamalar:

* **`{i18n>showHelloButtonText}`** → i18n modelindeki `showHelloButtonText` değerini çeker.
* i18n binding’de `/` kullanılmaz çünkü bu **flat key-value** yapısıdır.
* Input `description` kısmı burada sabit bırakıldı (örnek basit tutmak için).
  Gerçek projelerde bu da i18n’den alınmalıdır.

---

## 4️⃣ Klasör Yapısı

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
     ├───i18n
     │     i18n.properties
     │
     ├───view
     │     App.view.xml
     │
     └───controller
           App.controller.js
```

---

## 5️⃣ Terminal Çalıştırma

```powershell
cd C:\sapui5\SAPUI5_TUTORIALS\hello_world
npm start
```

* Tarayıcıda buton metni **Say Hello** olarak i18n’den gelecek.
* Butona basıldığında, modelden aldığı isim ile **Hello World** veya **Hello \[girilen isim]** mesajı görünecek.

---

## Konvansiyonlar

* i18n için **`ResourceModel`** kullanılır.
* Varsayılan dosya adı → `i18n.properties`
* Key’ler **lowerCamelCase** yazılır.
* Dinamik metinler `{0}`, `{1}`, `{2}` vb. parametreler ile tanımlanır.
* Çeviri metinleri asla string birleştirme ile yapılmaz → Her zaman `getText` + parametre kullanılır.
* Özel karakterler için **Unicode escape** (`\uXXXX`) kullanılır.

---

## Sonuç

Bu adımda:

* Sabit UI metinlerini i18n dosyasına taşıdık.
* Uygulamanın çok dilli desteği için temel altyapıyı kurduk.
* Controller ve View içinde i18n binding kullandık.

```
