# Step 9: Component Configuration

https://sapui5.hana.ondemand.com/#/topic/4cfa60872dca462cb87148ccd0d948ee

Bu adımda, uygulamanın tüm UI (kullanıcı arayüzü) bileşenlerini **Component** yapısı içine alıyoruz. Böylece uygulamamız **index.html**’den bağımsız, modüler ve yeniden kullanılabilir bir hale geliyor.

Bu yapı sayesinde uygulama SAP Fiori Launchpad gibi farklı ortamlarda da çalışabilir.

---

## 📂 Klasör Yapısı

Bu adımın sonunda proje yapınız şu şekilde olur:

```
webapp/
│
├── Component.js
├── controller/
│   └── App.controller.js
├── view/
│   └── App.view.xml
├── i18n/
│   └── i18n.properties
├── index.js
└── index.html
```

---

## 1️⃣ Component.js Oluşturma

**Amaç:** Uygulamanın başlangıç yapılandırmasını yapmak, model ve view tanımlarını merkezi hale getirmek.

**Dosya:** `webapp/Component.js`

```javascript
sap.ui.define([
   "sap/ui/core/UIComponent",
   "sap/ui/model/json/JSONModel",
   "sap/ui/model/resource/ResourceModel"
], (UIComponent, JSONModel, ResourceModel) => {
   "use strict";

   return UIComponent.extend("ui5.walkthrough.Component", {
      metadata : {
         "interfaces": ["sap.ui.core.IAsyncContentCreation"],
         "rootView": {
            "viewName": "ui5.walkthrough.view.App",
            "type": "XML",
            "id": "app"
         }
      },

      init() {
         // Parent init çağrısı
         UIComponent.prototype.init.apply(this, arguments);

         // JSON model ekleme
         const oData = {
            recipient : { name : "World" }
         };
         const oModel = new JSONModel(oData);
         this.setModel(oModel);

         // i18n model ekleme
         const i18nModel = new ResourceModel({
            bundleName: "ui5.walkthrough.i18n.i18n"
         });
         this.setModel(i18nModel, "i18n");
      }
   });
});
```

✅ **Açıklama:**

* **metadata.rootView** → Uygulamanın ana view'ını tanımlar.
* **init()** → Uygulama başlatıldığında çalışır, modeller burada tanımlanır.
* Modeller **Component** üzerinde tanımlandığı için tüm view’lar bunlara otomatik erişebilir.

---

## 2️⃣ App.controller.js Güncelleme

**Değişiklik:** `onInit` fonksiyonu ve model tanımlamaları artık **Component** içinde yapıldığı için kaldırılır.

**Dosya:** `webapp/controller/App.controller.js`

```javascript
sap.ui.define([
   "sap/ui/core/mvc/Controller",
   "sap/m/MessageToast"
], (Controller, MessageToast) => {
   "use strict";

   return Controller.extend("ui5.walkthrough.controller.App", {
      onShowHello() {
         const oBundle = this.getView().getModel("i18n").getResourceBundle();
         const sRecipient = this.getView().getModel().getProperty("/recipient/name");
         const sMsg = oBundle.getText("helloMsg", [sRecipient]);

         MessageToast.show(sMsg);
      }
   });
});
```

✅ **Açıklama:**
Artık model erişimleri **Component** üzerinden miras alınır, tekrar tanımlamaya gerek yoktur.

---

## 3️⃣ index.js Güncelleme

**Amaç:** View doğrudan yüklemek yerine Component kullanmak.

**Dosya:** `webapp/index.js`

```javascript
sap.ui.define([
	"sap/ui/core/ComponentContainer"
], (ComponentContainer) => {
	"use strict";

	new ComponentContainer({
		name: "ui5.walkthrough",
		settings : {
			id : "walkthrough"
		},
		async: true
	}).placeAt("content");
});
```

✅ **Açıklama:**

* `ComponentContainer` → Component'i yükler ve HTML içindeki `id="content"` elementine yerleştirir.
* `async: true` → Asenkron yükleme sağlar, performans iyileştirir.

---

## 📌 Özet

* **Component.js** tüm model, view ve yapılandırma ayarlarının merkezi noktası oldu.
* **Controller** daha temiz hale geldi, sadece olay yönetimi içeriyor.
* Uygulama **index.js** üzerinden Component olarak başlatılıyor.
* Bu mimari, uygulamanın SAP Fiori Launchpad gibi ortamlarda kolayca çalışmasını sağlar.

---

