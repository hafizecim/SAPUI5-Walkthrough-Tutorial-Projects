# Step 6: Modules

https://sapui5.hana.ondemand.com/#/topic/f665d0de4dba405f9af4294de824b03b

## Genel Bakış
Bu adımda, Step 5’te kullandığımız **alert** fonksiyonunu kaldırıp, onun yerine SAPUI5’in **sap.m.MessageToast** bileşenini kullanacağız.  
`MessageToast`, ekranın alt kısmında kısa süreli bilgilendirme mesajları göstermek için kullanılır.

---

## Adım Adım

### 1️⃣ Controller Güncelleme
`webapp/controller/App.controller.js` dosyasını aşağıdaki gibi değiştirin:

```javascript
sap.ui.define([
   "sap/ui/core/mvc/Controller",
   "sap/m/MessageToast"
], (Controller, MessageToast) => {
   "use strict";

   return Controller.extend("ui5.walkthrough.controller.App", {
      onShowHello() {
         MessageToast.show("Hello World");
      }
   });
});
````

**Açıklama:**

* `sap.ui.define([...], function(...){})` → SAPUI5’te modül tanımlama yöntemi (**Asynchronous Module Definition - AMD**).
* İlk parametre dizisinde (`[ ... ]`) yüklenmesini istediğimiz modüllerin **tam yollarını** yazıyoruz.

  * `"sap/ui/core/mvc/Controller"` → Controller sınıfı.
  * `"sap/m/MessageToast"` → Mesaj gösterme bileşeni.
* Callback fonksiyonundaki parametre isimleri (`Controller`, `MessageToast`) → Modüllere **kısa isim** veriyoruz.

  * Not: Parametre isimleri **namespace içermemeli**.
* `MessageToast.show("Hello World")` → Alt kısımda kısa süreli bir mesaj kutusu gösterir.

---

## 2️⃣ sap.ui.define ve sap.ui.require Farkı

* **sap.ui.define** → Bir modülü tanımlar ve global namespace’e ekler.
  Controller, Component gibi yeniden kullanılacak kodlarda tercih edilir.
* **sap.ui.require** → Modülü **asenkron** olarak yükler ama namespace oluşturmaz.
  Anlık çalıştırılacak kodlarda kullanılır.

---

## 3️⃣ Terminal Komutları

1. Proje klasörüne gidin:

   ```powershell
   cd C:\sapui5\SAPUI5_TUTORIALS\hello_world
   ```
2. UI5 sunucusunu başlatın:

   ```powershell
   npm start
   ```
3. Tarayıcıda uygulamayı açın → "Say Hello" butonuna basıldığında ekranın alt kısmında **Hello World** mesajı belirecek.

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
     ├───view
     │     App.view.xml
     │
     └───controller
           App.controller.js
```

---

## Konvansiyonlar

* **Modül tanımlamalarında** daima `sap.ui.define` kullanın.
* Parametre isimleri **namespace içermeden** kısa ve anlamlı olmalı (`MessageToast`, `Controller` gibi).
* Tekrar kullanılmayacak kodlar için `sap.ui.require` kullanılabilir.

---

## Sonuç

Bu adımda:

* **alert** yerine **MessageToast** kullandık.
* SAPUI5 modül yönetimi mantığını (**AMD**) öğrenmiş olduk.

```

