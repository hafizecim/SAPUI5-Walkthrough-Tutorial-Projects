# SAPUI5 Walkthrough - Adım 24: Sorting and Grouping

https://sapui5.hana.ondemand.com/#/topic/c4b2a32bb72f483faa173e890e48d812

Bu adımda, **fatura listesini sıralama ve gruplama** ile daha kullanıcı dostu hâle getiriyoruz.  
- Liste öğeleri alfabetik olarak sıralanır.  
- Öğeler, gönderici şirketine göre gruplandırılır.

---

## 1. Amaç
- Ürünleri alfabetik sırayla listelemek.  
- Gönderici şirketine göre gruplama yapmak.  
- SAPUI5’in `sorter` ve `group` özelliklerini kullanmak.

---

## 2. Basit Sıralama

### 📂 `webapp/view/InvoiceList.view.xml`
```xml
<List
    id="invoiceList"
    class="sapUiResponsiveMargin"
    width="auto"
    items="{
        path : 'invoice>/Invoices',
        sorter : {
            path : 'ProductName' 
        }
    }" >
    ...
</List>
````

📌 **Açıklama:**

* `path` → JSON model içindeki öğelere bağlanır.
* `sorter` → Öğeleri sıralamak için kullanılır.
* Varsayılan sıralama **ascending (artan)**.
* `descending: true` eklenirse azalan sırayla gösterilir.

---

## 3. Gruba Göre Sıralama ve Gruplama

### 📂 `webapp/view/InvoiceList.view.xml`

```xml
<List
    id="invoiceList"
    headerText="{i18n>invoiceListTitle}"
    class="sapUiResponsiveMargin"
    width="auto"
    items="{
        path : 'invoice>/Invoices',
        sorter : {
            path : 'ShipperName',
            group : true
        }
    }">
    ...
</List>
```

📌 **Açıklama:**

* `path: 'ShipperName'` → Gruplama, gönderici şirketine göre yapılır.
* `group: true` → SAPUI5 otomatik olarak grupları oluşturur ve başlık ekler.
* Ek bir işlem yapmaya gerek yok; `groupHeaderFactory` ile özel grup başlığı tasarlanabilir, fakat varsayılan görünüm yeterlidir.

---

## 4. Sonuç

* Liste artık gönderici şirketine göre gruplandırılmış ve alfabetik olarak sıralanmış hâlde görüntülenir.
* SAPUI5’in data binding özellikleri sayesinde grup başlıkları otomatik olarak oluşturulur.
* Kullanıcı, hangi şirketten hangi ürünlerin gönderildiğini kolayca görebilir.

---

## 5. Dosya Yapısı Özet

```
webapp/
├── view/
│   └── InvoiceList.view.xml   # sorter ve group eklendi
├── controller/
│   └── InvoiceList.controller.js
└── i18n/
    └── i18n.properties
```

---

## 6. Öneriler

* Sıralama ve gruplamayı birden fazla alanla birleştirebilirsiniz.
* Özel grup başlıkları için `groupHeaderFactory` kullanılabilir.
* JSON dışında OData modellerinde de aynı yöntemlerle gruplama ve sıralama uygulanabilir.

---

```
