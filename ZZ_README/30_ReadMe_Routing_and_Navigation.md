# Adım 30: Routing ve Navigasyon

https://sapui5.hana.ondemand.com/#/topic/e5200ee755f344c8aef8efcbab3308fb

Artık tüm uygulama içeriğini tek bir sayfada göstermiyoruz. Uygulama büyüdükçe içerikleri ayrı sayfalara ayırmak istiyoruz.  
Bu adımda, SAPUI5 **router** özelliğini kullanarak ayrı bir detay sayfası oluşturacak ve URL’i otomatik olarak güncelleyeceğiz.

---

## 1. Routing Yapılandırması (manifest.json)

```json
"sap.ui5": {
  "routing": {
    "config": {
      "routerClass": "sap.m.routing.Router",
      "type": "View",
      "viewType": "XML",
      "path": "ui5.walkthrough.view",
      "controlId": "app",
      "controlAggregation": "pages"
    },
    "routes": [
      {
        "pattern": "",
        "name": "overview",
        "target": "overview"
      },
      {
        "pattern": "detail",
        "name": "detail",
        "target": "detail"
      }
    ],
    "targets": {
      "overview": { "id": "overview", "name": "Overview" },
      "detail": { "id": "detail", "name": "Detail" }
    }
  }
}
````

* **config:** Router sınıfı, view yolu ve hangi kontrolün sayfaları göstereceğini belirtir.
* **routes:** URL desenlerini ve hedef sayfaları tanımlar.
* **targets:** Her route için gösterilecek view’leri tanımlar.

---

## 2. Component.js

```javascript
this.getRouter().initialize();
```

* Router otomatik olarak AppDescriptor yapılandırmasına göre başlatılır.
* URL değerlendirilir ve ilgili view yüklenir.

---

## 3. Overview View (Yeni)

`Overview.view.xml` içerisine önceki adımlardaki içerikler taşındı:

```xml
<mvc:View>
  <Page title="{i18n>homePageTitle}">
    <content>
      <mvc:XMLView viewName="ui5.walkthrough.view.HelloPanel" />
      <mvc:XMLView viewName="ui5.walkthrough.view.InvoiceList" />
    </content>
  </Page>
</mvc:View>
```

* Controller değişmedi, `ui5.walkthrough.controller.App` tekrar kullanıldı.

---

## 4. App View

`App.view.xml` artık sadece boş bir `<App>` içeriyor. Router, mevcut URL’e uygun view’i otomatik olarak ekler.

---

## 5. Detail View (Yeni)

`Detail.view.xml` sadece bir sayfa ve ObjectHeader içerir:

```xml
<mvc:View>
  <Page title="{i18n>detailPageTitle}">
    <ObjectHeader title="Invoice"/>
  </Page>
</mvc:View>
```

* Detail sayfası başlığı için `i18n` içerisine yeni string eklendi:

```
detailPageTitle=Walkthrough - Details
```

---

## 6. Invoice List View

* `ObjectListItem` tipini **Navigation** olarak ayarladık.
* `press` eventi ekledik:

```xml
<ObjectListItem
    type="Navigation"
    press=".onPress">
</ObjectListItem>
```

---

## 7. InvoiceList.controller.js

```javascript
onPress() {
  const oRouter = this.getOwnerComponent().getRouter();
  oRouter.navTo("detail");
}
```

* Listeden bir öğe tıklandığında **detail** sayfasına navigasyon yapılır.

---

## Konvansiyonlar

* Routing yapılandırmasını manifest.json içinde tanımlayın.
* Router’ı Component#init içinde başlatın.

---

**Önceki Adım:** Step 29: Debugging Tools
**Sonraki Adım:** Step 31: Routing with Parameters
**İlgili Kaynaklar:**

* [Routing and Navigation](https://sapui5.hana.ondemand.com/#/topic/…)
* [Tutorial: Navigation and Routing](https://sapui5.hana.ondemand.com/#/topic/…)

```

