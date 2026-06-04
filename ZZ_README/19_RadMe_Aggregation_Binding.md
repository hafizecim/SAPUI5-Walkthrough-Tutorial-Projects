# SAPUI5 Walkthrough - Adım 19: Aggregation Binding

https://sapui5.hana.ondemand.com/#/topic/bf71375454654b44af01379a3c3a6273

Bu adımda uygulamaya **fatura listesi** ekleyerek **aggregation binding** kavramını öğreniyoruz.  
JSON formatında verilerimizi tanımlıyor ve `List` kontrolü ile ekrana bağlıyoruz.

---

## 1. Amaç
- Uygulamaya **JSON veri modeli** eklemek.
- **Named model** kullanmak.
- Bir `List` kontrolünde **aggregation binding** ile veri göstermek.

---

## 2. Yeni ve Güncellenen Dosyalar

### 📂 `webapp/Invoices.json` _(Yeni)_
```json
{
  "Invoices": [
    {
      "ProductName": "Pineapple",
      "Quantity": 21,
      "ExtendedPrice": 87.2,
      "ShipperName": "Fun Inc.",
      "ShippedDate": "2015-04-01T00:00:00",
      "Status": "A"
    },
    {
      "ProductName": "Milk",
      "Quantity": 4,
      "ExtendedPrice": 10,
      "ShipperName": "ACME",
      "ShippedDate": "2015-02-18T00:00:00",
      "Status": "B"
    },
    {
      "ProductName": "Canned Beans",
      "Quantity": 3,
      "ExtendedPrice": 6.85,
      "ShipperName": "ACME",
      "ShippedDate": "2015-03-02T00:00:00",
      "Status": "B"
    },
    {
      "ProductName": "Salad",
      "Quantity": 2,
      "ExtendedPrice": 8.8,
      "ShipperName": "ACME",
      "ShippedDate": "2015-04-12T00:00:00",
      "Status": "C"
    },
    {
      "ProductName": "Bread",
      "Quantity": 1,
      "ExtendedPrice": 2.71,
      "ShipperName": "Fun Inc.",
      "ShippedDate": "2015-01-27T00:00:00",
      "Status": "A"
    }
  ]
}
````

📌 **Açıklama:**

* Basit bir fatura listesi içerir.
* JSONModel tarafından doğrudan veri kaynağı olarak kullanılabilir.

---

### 📂 `webapp/manifest.json` *(Güncellendi)*

```json
{
  ...
  "sap.ui5": {
    ...
    "models": {
      "i18n": {
        "type": "sap.ui.model.resource.ResourceModel",
        "settings": {
          "bundleName": "ui5.walkthrough.i18n.i18n",
          "supportedLocales": [""],
          "fallbackLocale": ""
        }
      },
      "invoice": {
        "type": "sap.ui.model.json.JSONModel",
        "uri": "Invoices.json"
      }
    }
  }
  ...
}
```

📌 **Açıklama:**

* `"invoice"` adında **named model** oluşturuldu.
* `"type"` → `sap.ui.model.json.JSONModel`
* `"uri"` → `Invoices.json` dosyası.

---

### 📂 `webapp/view/App.view.xml` *(Güncellendi)*

```xml
<mvc:View
	controllerName="ui5.walkthrough.controller.App"
	xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc"
	displayBlock="true">
    <Shell>
        <App class="myAppDemoWT">
            <pages>
                <Page title="{i18n>homePageTitle}">
                    <content>
                        <Panel
                            headerText="{i18n>helloPanelTitle}"
                            class="sapUiResponsiveMargin"
                            width="auto">
                            <content>
                                <mvc:XMLView
                                    viewName="ui5.walkthrough.view.HelloPanel"/>
                                <mvc:XMLView
                                    viewName="ui5.walkthrough.view.InvoiceList"/>
                            </content>
                        </Panel>
                    </content>
                </Page>
            </pages>
        </App>
    </Shell>
</mvc:View>
```

📌 **Açıklama:**

* `HelloPanel` altında `InvoiceList` görünümü eklendi.

---

### 📂 `webapp/view/InvoiceList.view.xml` *(Yeni)*

```xml
<mvc:View
   xmlns="sap.m"
   xmlns:mvc="sap.ui.core.mvc">
   <List
      headerText="{i18n>invoiceListTitle}"
      class="sapUiResponsiveMargin"
      width="auto"
      items="{invoice>/Invoices}" >
      <items>
         <ObjectListItem
            title="{invoice>Quantity} x {invoice>ProductName}"/>
      </items>
   </List>
</mvc:View>
```

📌 **Açıklama:**

* `items="{invoice>/Invoices}"` → **Aggregation binding**.
* `ObjectListItem` → Her bir fatura için tekrar eden şablon.
* `invoice>` ön eki → Named model kullanıldığını gösterir.

---

### 📂 `webapp/i18n/i18n.properties` *(Güncellendi)*

```properties
# Invoice List
invoiceListTitle=Invoices
```

📌 **Açıklama:**

* Liste başlığı i18n üzerinden sağlandı.

---

## 3. Aggregation Binding Mantığı

* `items` aggregation → JSON modeldeki `Invoices` dizisine bağlandı.
* **Relative path** kullanıldığı için (`invoice>Quantity`) otomatik olarak o item’in verisi alınır.
* Şablon (`ObjectListItem`) her veri satırı için tekrar oluşturulur.

---

## 4. Terminal Komutları

```sh
npm start
```

veya

```sh
ui5 serve
```

Sonrasında tarayıcıda:

```
http://localhost:8080
```

---

## 5. Dosya Yapısı

```
C:\sapui5\SAPUI5_TUTORIALS\hello_world\
│
├── webapp\
│   ├── controller\
│   │   └── App.controller.js
│   ├── view\
│   │   ├── App.view.xml              # Güncellendi
│   │   ├── HelloPanel.view.xml
│   │   └── InvoiceList.view.xml      # Yeni
│   ├── i18n\
│   │   └── i18n.properties           # Güncellendi
│   ├── Invoices.json                 # Yeni
│   ├── manifest.json                 # Güncellendi
│   └── index.html
└── package.json
```

---

## 6. Sonuç

Bu adımda:

* `invoice` adında **named JSON model** tanımlandı.
* `Invoices.json` dosyası veri kaynağı olarak bağlandı.
* `InvoiceList` view oluşturularak aggregation binding ile listelendi.
* Uygulama artık **dinamik veri tabanlı** çalışmaya başladı.

---

