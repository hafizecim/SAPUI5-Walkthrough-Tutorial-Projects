# Step 2: Bootstrap

https://sapui5.hana.ondemand.com/#/topic/fe12df2e338e43598977d09f3d191b7b

## Genel Bakış
Bu adımda SAPUI5’in **yüklenmesi ve başlatılması** öğretiliyor. Bu işleme **bootstrapping** denir. Bootstrapping tamamlandığında basit bir alert ile SAPUI5’in hazır olduğunu göstereceğiz.  

---

## Adım Adım

### 1️⃣ UI5 Tooling Kurulumunu Geliştirme
- Terminali **app root folder** olan `C:\sapui5\SAPUI5_TUTORIALS\hello_world` klasöründe açın.  
- Aşağıdaki komutları çalıştırın:  
  ```powershell
  ui5 use OpenUI5
  ui5 add sap.ui.core sap.m themelib_sap_horizon


* Bu komutlar ne yapar:
--> ui5.yaml dosyas günceller
  * `sap.ui.core`: SAPUI5’in temel kütüphanesini yükler.  
  * `sap.m`: Mobil ve web kontrollerini içeren kütüphane.
  * `themelib_sap_horizon`: SAPUI5’in Horizon temasını ekler, uygulamanın görünümünü belirler.

---

### 2️⃣ index.html Dosyasına Bootstrap Scripti Eklemek

* `webapp/index.html` dosyasını açın ve `<head>` kısmına **bootstrap scripti** ekleyin.

* Script ne yapar:

  * SAPUI5 kütüphanesini web sunucusundan yükler.
  * Tanımlanan kütüphaneleri (`sap.m`) ve temayı (`sap_horizon`) uygular.
  * Uygulama için başlangıç modülünü (`index.js`) çalıştırır.
  * JavaScript kodunu doğrudan HTML içine yazmak yerine **modül olarak yükler**, bu daha güvenlidir.

* Scriptin önemli özellikleri:

  * `id="sap-ui-bootstrap"` → SAPUI5’in doğru şekilde başlatılmasını sağlar.
  * `data-sap-ui-async="true"` → Kütüphaneleri arka planda eş zamanlı yükler, performansı artırır.
  * `data-sap-ui-on-init="module:ui5/walkthrough/index"` → Başlangıç modülünü belirtir.
  * `data-sap-ui-resource-roots` → `ui5.walkthrough` namespace’ini klasörle eşleştirir.

---

### 3️⃣ index.js Dosyası Oluşturmak

* `webapp/index.js` dosyasını oluşturun.

* Bu dosya uygulama mantığını içerir.

* İlk adımda basit olarak:

  ```javascript
  alert("UI5 is ready");
  ```

  gösterecek şekilde yapılandırılır.

* Amaç:

  * Uygulama mantığını **HTML’den ayırmak**.
  * Kod modül olarak yüklendiği için güvenliği artırmak.

---

## Terminalde Yapılacaklar

1. Proje kök klasörüne gitmek:

   ```powershell
   cd C:\sapui5\SAPUI5_TUTORIALS\hello_world
   ```
2. UI5 Tooling komutlarını çalıştırmak:

   ```powershell
   ui5 use OpenUI5
   ui5 add sap.ui.core sap.m themelib_sap_horizon
   ```
3. Uygulamayı çalıştırmak (önce package.json ve ui5.yaml hazırsa):

   ```powershell
   npm start
   ```
4. Tarayıcıda `index.html` açılır ve "UI5 is ready" alert’i görünür.

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

```

