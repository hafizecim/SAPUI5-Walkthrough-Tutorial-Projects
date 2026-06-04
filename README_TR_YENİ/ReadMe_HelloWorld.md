# SAPUI5 Walkthrough Öğrenme Projesi

## Genel Bakış

Bu depo, SAPUI5/OpenUI5 resmi Walkthrough eğitiminin adım adım uygulanmasını içermektedir.

Her eğitim adımı için ayrı bir proje oluşturmak yerine, tek bir SAPUI5 uygulaması geliştirilmekte ve eğitim boyunca sürekli olarak büyütülmektedir.

Tamamlanan her adım GitHub'a commit edilerek uygulamanın basit bir "Hello World" ekranından tam kapsamlı bir SAPUI5 uygulamasına dönüşümü takip edilebilmektedir.

---

## Proje Yapısı

```text
SAPUI5_TUTORIALS
│
├── package.json
├── package-lock.json
├── ui5.yaml
├── README.md
│
└── webapp
    ├── index.html
    ├── manifest.json
    └── ...
```

---

## Adım 1 – Hello World

### Klasör Yapısı

```text
1. Ana klasörü oluştur:
   SAPUI5_TUTORIALS

2. SAPUI5_TUTORIALS altında oluştur:
   webapp

3. webapp altında oluştur:
   index.html
   manifest.json

4. SAPUI5_TUTORIALS altında oluştur:
   package.json
```

---

### webapp/index.html Dosyasını Oluştur

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>UI5 TypeScript Walkthrough</title>
</head>
<body>
    <div>Hello World</div>
</body>
</html>
```

---

### webapp/manifest.json Dosyasını Oluştur

```json
{
    "_version": "1.60.0",
    "sap.app": {
        "id": "ui5.walkthrough",
        "type": "application",
        "title": "OpenUI5 TypeScript Walkthrough",
        "applicationVersion": {
            "version": "1.0.0"
        }
    }
}
```

---

### package.json Dosyasını Oluştur

```json
{
    "name": "ui5.walkthrough",
    "version": "1.0.0",
    "description": "OpenUI5 TypeScript Walkthrough",
    "private": true,
    "scripts": {
        "start": "ui5 serve -o index.html"
    }
}
```

---

## Kurulum

Proje ana dizininde terminal açın:

```bash
cd C:\sapui5\SAPUI5_TUTORIALS
```

UI5 CLI paketini yükleyin:

```bash
npm install --save-dev @ui5/cli
```

UI5 yapılandırmasını oluşturun:

```bash
ui5 init
```

Geliştirme sunucusunu başlatın:

```bash
npm start
```

---

## Eğitim İlerleme Durumu

* [x] Adım 1: Hello World
* [ ] Adım 2: Bootstrap
* [ ] Adım 3: Controls
* [ ] Adım 4: XML Views
* [ ] Adım 5: Controllers
* [ ] Adım 6: Modules
* [ ] Adım 7: JSON Model
* [ ] Adım 8: Translatable Texts
* [ ] Adım 9: Component Configuration
* [ ] Adım 10: Descriptor for Applications
* [ ] Adım 11: Pages and Panels
* [ ] Adım 12: Shell Control as Container
* [ ] Adım 13: Margins and Paddings
* [ ] Adım 14: Custom CSS and Theme Colors
* [ ] Adım 15: Nested Views
* [ ] Adım 16: Dialogs and Fragments
* [ ] Adım 17: Fragment Callbacks
* [ ] Adım 18: Icons
* [ ] Adım 19: Aggregation Binding
* [ ] Adım 20: Data Types
* [ ] Adım 21: Expression Binding
* [ ] Adım 22: Custom Formatters
* [ ] Adım 23: Filtering
* [ ] Adım 24: Sorting and Grouping
* [ ] Adım 25: Remote OData Service
* [ ] Adım 26: Mock Server Configuration
* [ ] Adım 27: Unit Test with QUnit
* [ ] Adım 28: Integration Test with OPA
* [ ] Adım 29: Debugging Tools
* [ ] Adım 30: Routing and Navigation
* [ ] Adım 31: Routing with Parameters
* [ ] Adım 32: Routing Back and History
* [ ] Adım 33: Custom Controls
* [ ] Adım 34: Responsiveness
* [ ] Adım 35: Device Adaptation
* [ ] Adım 36: Content Density
* [ ] Adım 37: Accessibility
* [ ] Adım 38: Build Your Application

---

## Öğrenme Yaklaşımı

Bu depoda eğitim boyunca tek bir proje kullanılmaktadır.

Her yeni eğitim adımı, bir önceki adımın üzerine eklenerek ilerler. Böylece gerçek SAPUI5 kurumsal uygulama geliştirme sürecine benzer bir çalışma yöntemi uygulanır.

Her önemli aşama GitHub'a commit edilerek uygulamanın gelişim süreci commit geçmişi üzerinden takip edilebilir.

---

## Amaç

Bu proje sayesinde aşağıdaki konularda deneyim kazanılması hedeflenmektedir:

* SAPUI5 Temelleri
* UI5 CLI Kullanımı
* MVC Mimarisi
* XML Views
* Controllers
* Models
* Data Binding
* Routing
* OData Servisleri
* Test Süreçleri (QUnit & OPA)
* Responsive Tasarım
* SAPUI5 En İyi Uygulamaları
