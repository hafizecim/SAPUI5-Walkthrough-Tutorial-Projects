# Step 5: Controllers

https://sapui5.hana.ondemand.com/#/topic/50579ddf2c934ce789e056cfffe9efa9

## Genel Bakış
Bu adımda, XML View’deki **Text** kontrolünü **Button** ile değiştirip, butona tıklandığında **"Hello World"** mesajı göstereceğiz.  
Butonun **event handling** (olay yönetimi) kısmı, View’e bağlı **Controller** içinde tanımlanacak.

---

## Adım Adım

### 1️⃣ View Güncelleme
`webapp/view/App.view.xml` dosyasını şu şekilde düzenleyin:
```xml
<mvc:View
   controllerName="ui5.walkthrough.controller.App"
   xmlns="sap.m"
   xmlns:mvc="sap.ui.core.mvc">
   <Button
      text="Say Hello"
      press=".onShowHello"/>
</mvc:View>
````

**Açıklama:**

* `controllerName` → View’in hangi Controller ile ilişkilendirileceğini belirtir.

  * Format: `namespace.controller.ControllerAdi`
  * Bizim örneğimizde: `ui5.walkthrough.controller.App`
* `<Button>` kontrolü:

  * `text="Say Hello"` → Butonun üzerinde gözüken yazı.
  * `press=".onShowHello"` → Butona tıklandığında çalışacak fonksiyon (Controller içinde tanımlanır).
* **Nokta (`.`)** ile başlayan event handler isimleri (`.onShowHello`), View’in kendi Controller’ında aranır.

---

### 2️⃣ Controller Oluşturma

Yeni bir klasör oluşturun:

```
webapp/controller
```

İçine `App.controller.js` dosyası ekleyin:

```javascript
sap.ui.define([
   "sap/ui/core/mvc/Controller"
], (Controller) => {
   "use strict";

   return Controller.extend("ui5.walkthrough.controller.App", {
      onShowHello() {
         // Native JavaScript alert ile mesaj göster
         alert("Hello World");
      }
   });
});
```

**Açıklama:**

* `"sap/ui/core/mvc/Controller"` → UI5’in temel Controller sınıfı.
* `Controller.extend("...")` → Kendi Controller’ımızı oluşturur.
* `onShowHello()` → Butonun `press` event’ine bağlanan fonksiyon.
* `alert("Hello World")` → Basit bir tarayıcı uyarı penceresi.

---

## Konvansiyonlar

* **Controller isimleri büyük harfle** başlar (örn. `App.controller.js`).
* Controller dosya isimleri View ile **aynı ada** sahip olmalı (1:1 ilişki varsa).
* Event handler fonksiyonları **on** ile başlamalı (`onShowHello`, `onInit` vb.).
* Controller dosya uzantısı her zaman **.controller.js** olmalı.

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
3. Tarayıcıda uygulamayı açın → "Say Hello" butonuna basıldığında **Hello World** alert penceresi görünür.

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
     ├───view
     │     App.view.xml
     │
     └───controller
           App.controller.js
```

---

## Notlar

* View sadece UI tanımı içerir, Controller ise olayları (event) ve iş mantığını yönetir.
* `controllerName` View ile Controller arasında köprü görevi görür.
* Bu adımda **MVC** yapısının “Controller” kısmı aktif olarak kullanılmaya başlanmış oldu.

```

