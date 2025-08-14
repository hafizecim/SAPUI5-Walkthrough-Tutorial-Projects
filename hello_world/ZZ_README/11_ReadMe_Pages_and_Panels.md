# Step 11: Pages and Panels

https://sapui5.hana.ondemand.com/#/topic/3b9d9f84930d43df90ad0789d99bd4a3

Bu adımda, uygulamanın görünümünü **sap.m** kütüphanesinden gelen **Page** ve **Panel** kontrollerini kullanarak geliştireceğiz. Böylece UI, hem daha düzenli hem de daha profesyonel görünecek. Ayrıca kontrol *aggregation* mantığını da öğreneceğiz.

---

## 🎯 Amaç
- Buton ve giriş alanını bir panel içinde gruplayarak düzenli bir görünüm elde etmek.
- Uygulama içeriğini **Page** yapısına yerleştirip başlık eklemek.
- **App** kontrolü ile mobil uyumlu yapı sağlamak.

---

## 📂 Güncellenen Dosya

**`webapp/view/App.view.xml`**
```xml
<mvc:View
   controllerName="ui5.walkthrough.controller.App"
   xmlns="sap.m"
   xmlns:mvc="sap.ui.core.mvc"
   displayBlock="true">
   <App>
      <pages>
         <Page title="{i18n>homePageTitle}">
            <content>
               <Panel headerText="{i18n>helloPanelTitle}">
                  <content>
                     <Button
                        text="{i18n>showHelloButtonText}"
                        press=".onShowHello"/>
                     <Input
                        value="{/recipient/name}"
                        description="Hello {/recipient/name}"
                        valueLiveUpdate="true"
                        width="60%"/>
                  </content>
               </Panel>
            </content>
         </Page>
      </pages>
   </App>
</mvc:View>
````

---

## 📂 Güncellenen Çeviri Dosyası

**`webapp/i18n/i18n.properties`**

```properties
# App Descriptor
appTitle=Hello World
appDescription=A simple walkthrough app that explains the most important concepts of SAPUI5

# Hello Panel
showHelloButtonText=Say Hello
helloMsg=Hello {0}
homePageTitle=Walkthrough
helloPanelTitle=Hello World
```

---

## 📖 Açıklamalar

* **sap.m.App**

  * Mobil uyumluluk için gerekli meta bilgileri `index.html` içine ekler.
  * Sayfalar arası geçiş ve animasyon desteği sağlar.
* **sap.m.Page**

  * Uygulama içeriğini kapsar.
  * `title` özelliği ile üst başlık ekler.
  * `content` aggregation’ı ile birden fazla kontrol eklenebilir.
* **sap.m.Panel**

  * İlgili UI elemanlarını gruplar.
  * `headerText` özelliği ile başlık eklenebilir.
* **displayBlock="true"**

  * Görünümün tam ekran yüksekliğe sahip olmasını sağlar.

---

## 🔗 İlgili Kaynaklar

* [API Reference: sap.m.Page](https://ui5.sap.com/#/api/sap.m.Page)
* [API Reference: sap.m.Panel](https://ui5.sap.com/#/api/sap.m.Panel)
* [Samples: sap.m.NavContainer](https://ui5.sap.com/#/entity/sap.m.NavContainer)

```


