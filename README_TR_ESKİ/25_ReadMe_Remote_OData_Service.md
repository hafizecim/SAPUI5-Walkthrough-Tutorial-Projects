# Adım 25: Uzaktan OData Servisi

https://sapui5.hana.ondemand.com/#/topic/44062441f3bd4c67a4f665ae362d1109

Şimdiye kadar yerel JSON verileri ile çalıştık, fakat artık gerçek bir OData servisine bağlanarak uzak verileri görüntüleyeceğiz.

## Genel Bakış
Gerçek dünyada veriler genellikle uzak sunucularda bulunur ve OData servisleri aracılığıyla erişilir. Bu adımda, **JSONModel** tipi yerine herkese açık **Northwind OData servisi** kullanacağız.

> Not: Çalıştıramazsanız endişelenmeyin, sonraki adımlar yerel JSON verisiyle de çalışır. Step 26’da sahte bir sunucu (mock server) kullanmayı öğreneceğiz.

---

## 1. Proxy Sunucusunu Kurma
CORS (Cross-Origin Resource Sharing) sorunlarını önlemek için **UI5 Tooling** proxy kullanıyoruz.

Proje kök dizininde middleware’i kurun: Terminal ile 

```bash
npm i -D ui5-middleware-simpleproxy
````

`ui5.yaml` dosyasında proxy yapılandırması:

```yaml
server:
  customMiddleware:
    - name: ui5-middleware-simpleproxy
      afterMiddleware: compression
      mountPath: /V2
      configuration:
        baseUri: "https://services.odata.org"
```

* `mountPath`: Proxy’nin yakalayacağı URL’ler
* `baseUri`: Gerçek OData sunucu adresi

---

## 2. manifest.json Dosyasında Veri Kaynağı Tanımlama

```json
"sap.app": {
  "dataSources": {
    "invoiceRemote": {
      "uri": "V2/Northwind/Northwind.svc/",
      "type": "OData",
      "settings": {
        "odataVersion": "2.0"
      }
    }
  }
}
```

* `invoiceRemote`: Veri kaynağı anahtarı
* `uri`: Proxy üzerinden Northwind servisine yönlendirme
* `type`: OData servisi tipi
* `odataVersion`: 2.0

---

## 3. Modeli Veri Kaynağına Bağlama

`sap.ui5.models` içinde:

```json
"models": {
  "invoice": {
    "dataSource": "invoiceRemote"
  }
}
```

* SAPUI5 otomatik olarak bir `sap.ui.model.odata.v2.ODataModel` oluşturur
* Model adı `invoice` olup controller veya view’lerde kullanılabilir

---

## 4. Controller’da Modeli Kullanma

* Varsayılan model:

```javascript
this.getView().getModel();
```

* İsimli model:

```javascript
this.getView().getModel("invoice");
```

---

## Özet

* Yerel JSON verisi yerine **uzaktaki OData servisi** kullanıldı.
* **UI5 proxy** ile CORS sorunları çözüldü.
* Mevcut kodda minimum değişiklikle liste aynı şekilde çalışıyor.
* manifest.json üzerinden ODataModel otomatik olarak oluşturuluyor.

---

**Ana Konu:** Walkthrough Tutorial (JavaScript)
**Önceki:** Step 24: Sıralama ve Gruplama
**Sonraki:** Step 26: Sahte Sunucu (Mock Server) Yapılandırması

```


