# SAPUI5 Walkthrough - Adım 21: Expression Binding

https://sapui5.hana.ondemand.com/#/topic/c98d57347ba444c6945f596584d2db45

Bu adımda, SAPUI5’in **expression binding** özelliğini kullanarak fiyat değerlerine koşullu durum (state) atıyoruz.  
Amaç: Fiyat 50’den büyükse kırmızı, değilse yeşil gösterilecek.

---

## 1. Amaç
- Fiyat değerine göre görsel durum belirlemek (Error / Success).  
- **Expression binding** kullanarak küçük hesaplamalar veya koşullu biçimlendirme yapmak.  
- Tipik kullanım: renk, görünürlük, ikon durumu vb. küçük hesaplamalar.

---

## 2. Güncellenen Dosya

### 📂 `webapp/view/InvoiceList.view.xml`
```xml
<mvc:View
    controllerName="ui5.walkthrough.controller.InvoiceList"
    xmlns="sap.m"
    xmlns:core="sap.ui.core"
    xmlns:mvc="sap.ui.core.mvc">
    <List
        headerText="{i18n>invoiceListTitle}"
        class="sapUiResponsiveMargin"
        width="auto"
        items="{invoice>/Invoices}">
        <items>
            <ObjectListItem
                core:require="{
                    Currency: 'sap/ui/model/type/Currency'
                }"
                title="{invoice>Quantity} x {invoice>ProductName}"
                number="{
                    parts: [
                        'invoice>ExtendedPrice',
                        'view>/currency'
                    ],
                    type: 'Currency',
                    formatOptions: {
                        showMeasure: false
                    }
                }"
                numberUnit="{view>/currency}"
                numberState="{= ${invoice>ExtendedPrice} > 50 ? 'Error' : 'Success' }"/>
        </items>
    </List>
</mvc:View>
````

📌 **Açıklama:**

* `numberState` → ObjectListItem kontrolünün durumu (Error = kırmızı, Success = yeşil).
* `{= ... }` → Expression binding başlatır.
* `${invoice>ExtendedPrice}` → Model binding ifadesi, `$` işareti ile escape edilir.
* Ternary operator kullanımı:

  ```js
  ${invoice>ExtendedPrice} > 50 ? 'Error' : 'Success'
  ```
* Expression binding yalnızca küçük hesaplamalar ve basit mantıksal ifadeler için uygundur.

---

## 3. Sonuç

* Fiyat 50’den büyük olan fatura kırmızı (Error), diğerleri yeşil (Success) olarak gösterilir.
* Expression binding sayesinde view içinde küçük hesaplamalar ve koşullar uygulanabilir.

---

## 4. Öneriler

* Karmaşık işlemler için **formatter fonksiyonları** kullanın.
* Expression binding, yalnızca basit hesaplamalar ve koşullu durumlar için uygundur.

---

## 5. Dosya Yapısı Özet

```
webapp/
├── view/
│   └── InvoiceList.view.xml   # Güncellendi (Expression Binding eklendi)
├── controller/
│   └── InvoiceList.controller.js
└── Invoices.json
```

---
