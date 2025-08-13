# Step 7: JSON Model

https://sapui5.hana.ondemand.com/#/topic/70ef981d350a495b940640801701c409

## Genel Bakış
Artık **MVC** yapısında **M (Model)** kısmına geçiyoruz.  
Bu adımda uygulamamıza:
- Bir **Input** alanı ekleyeceğiz.
- Bu alanın değerini bir **JSON Model** ile bağlayacağız.
- Kullanıcı yazdıkça alt açıklama metni anında güncellenecek.

---

## 1️⃣ Controller Güncelleme

`webapp/controller/App.controller.js` dosyasını şu şekilde düzenleyin:

```javascript
sap.ui.define([
   "sap/ui/core/mvc/Controller",
   "sap/m/MessageToast",
   "sap/ui/model/json/JSONModel"
], (Controller, MessageToast, JSONModel) => {
   "use strict";

   return Controller.extend("ui5.walkthrough.controller.App", {
      onInit() {
         // Model verisini tanımla
         const oData = {
            recipient : {
               name : "World"
            }
         };

         // JSON Model oluştur
         const oModel = new JSONModel(oData);

         // View'a modeli ata
         this.getView().setModel(oModel);
      },

      onShowHello() {
         MessageToast.show("Hello World");
      }
   });
});
````

### Açıklamalar

* **`onInit()`**: SAPUI5’te controller yüklendiğinde **otomatik olarak** çalışır (lifecycle method).
* **`JSONModel`**: Veriyi JSON formatında saklamak ve UI’a bağlamak için kullanılır.
* **`this.getView().setModel(oModel)`**: Modeli ilgili View'a bağlar. Böylece XML View içinde model verisine erişebiliriz.

---

## 2️⃣ View Güncelleme

`webapp/view/App.view.xml` dosyasını şu şekilde güncelleyin:

```xml
<mvc:View
   controllerName="ui5.walkthrough.controller.App"
   xmlns="sap.m"
   xmlns:mvc="sap.ui.core.mvc">

   <Button
      text="Say Hello"
      press=".onShowHello"/>

   <Input
      value="{/recipient/name}"
      description="Hello {/recipient/name}"
      valueLiveUpdate="true"
      width="60%"/>
</mvc:View>
```

### Açıklamalar

* **`<Input>`**: Kullanıcıdan metin girmek için.
* **`value="{/recipient/name}"`** → Modeldeki `/recipient/name` alanına bağlanır.
  Bu bağlama türüne **data binding** denir.
* **`description="Hello {/recipient/name}"`** → Kullanıcı yazdıkça açıklama anında güncellenir.
* **`valueLiveUpdate="true"`** → Kullanıcı her karakter girdiğinde model anında güncellenir.

---

## 3️⃣ Klasör Yapısı

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
     ├───view
     │     App.view.xml
     │
     └───controller
           App.controller.js
```

---

## 4️⃣ Terminal Çalıştırma

1. Proje klasörüne gidin:

   ```powershell
   cd C:\sapui5\SAPUI5_TUTORIALS\hello_world
   ```
2. Sunucuyu başlatın:

   ```powershell
   npm start
   ```
3. Tarayıcıda uygulamayı açın:

   * "Say Hello" butonu çalışmalı.
   * Input alanına yazdığınız değer, açıklamada **anında** güncellenmeli.

---

## Konvansiyonlar

* Model verileri **JSONModel** ile yönetilir.
* View içindeki veri erişimleri **data binding** ile yapılır.
* `{}` süslü parantezler → Model verisine erişim.
* Model yolları (`/recipient/name`) **root (/) ile başlar**.

---

## Sonuç

Bu adımda:

* İlk **modelimizi** oluşturduk.
* View ile model arasında **iki yönlü veri bağlama** (two-way binding) yaptık.
* Kullanıcı etkileşimini modele bağladık.

```

