# Not şablonları ve onay özeti

Gövdeler Notion-flavored Markdown'dır. Başlık gövdeye yazılmaz (`Name` özelliğine gider).
Köşeli parantez içindeki yer tutucular doldurulur; `<!-- -->` yorumları çıktıya girmez.

## 1) Geçici Not

Amaç: fikri hızla, yapılandırılmış ve geri dönülebilir biçimde yakalamak. 80–250 kelime.

```
[Fikrin tek paragraflık özü: ne, neden önemli.]
<empty-block/>
## Ana Fikir
- [Fikrin çekirdeği, 1–3 madde]
<empty-block/>
## Nasıl Çalışır / Bileşenler
1. [Adım veya bileşen]
2. [Adım veya bileşen]
<empty-block/>
## Açık Sorular
- [Araştırılması veya doğrulanması gereken nokta]
<empty-block/>
## Sonraki Adım
[Literatür araştırması / prototip / görüşme vb. tek cümle]
```

Özellikler: `Kategori` = `Geçici Not`, `Kaynak` boş, `Bağlantılar` varsa ilgili notlar.

## 2) Literatür Not

Amaç: web kaynaklarından sentezlenmiş, atıflı konu notu. 300–900 kelime. Tek konu, tek not.

```
**[Kavram]**, [bir cümlelik tanım]. \[1\]
<empty-block/>
## 1. Temel Kavramlar
- **[Terim]:** [açıklama] \[1\]
- **[Terim]:** [açıklama] \[2\]
<empty-block/>
## 2. [Konuya özgü başlık: mekanizma / tarihçe / türler]
[Paragraflar; her alıntılanan iddia atıf taşır.] \[2\]\[3\]
<empty-block/>
## 3. [Uygulama / Örnekler / Tartışmalar]
- [Örnek veya karşıt görüş] \[4\]
<empty-block/>
## Değerlendirme
[Kaynakların uzlaştığı ve ayrıştığı noktalar; güvenilirlik notu; 2–4 cümle.]
<empty-block/>
## Kaynaklar
1. [Başlık] - [URL]
2. [Başlık] - [URL]
```

Özellikler:
- `Kategori` = `Literatür Not`
- `Kaynak` = gövdedeki "Kaynaklar" listesinin aynısı, satır başına `n. Başlık - URL`
- `Bağlantılar` = veritabanında aynı konuda mevcut notlar (mention)

Model kaynaklı varyant (kullanıcı açıkça isterse): aynı şablon, ancak "Kaynaklar" bölümü ve
`\[n\]` atıfları yok; `Kaynak` = model adı ve seviyesi (`Claude Fable 5.1 High`). Gövdeye
uyarı ya da "web kaynağı olmadan yazıldı" notu eklenmez.

Veri analizi çıktısında (`analiz` modu) başlıklar: `## Veri Seti`, `## Yöntem`,
`## Bulgular`, `## Görseller`, `## Sınırlılıklar`, `## Sonuç`; `Kaynak` =
`1. dosya.csv (1.240×12) - Tanımlayıcı istatistik + korelasyon`.

## 3) Zettelkasten (Kalıcı) Not

Amaç: tek bir fikrin kendi cümlelerle, kaynak notlara atıfla, kalıcı ifadesi. 120–400 kelime.

```
[Fikrin iddiası: tek cümle, net, savunulabilir.]
<empty-block/>
[Gerekçe: neden böyle? Kaynak notlardan sentez, her alıntı atıflı.] \[1\]
<empty-block/>
[Sonuç / uygulama: bu fikir neyi değiştirir, nerede kullanılır? Örnek.]
<empty-block/>
> [İsteğe bağlı: tek bir doğrudan alıntı, kaynağı ile] \[2\]
<empty-block/>
## İlgili Notlar
- <mention-page url="..."/> — [bu notla bağlantının bir cümlelik gerekçesi]
```

Özellikler:
- `Kategori` = `Zettelkasten`
- `Kaynak` = `1. <mention-page url="..."/>` satırları (kaynak notlar: literatür veya geçici)
- `Bağlantılar` = ilgili diğer notlar (mention); kaynak notlar buraya tekrar yazılmaz
- Başlık bir **önerme** olmalı ("X, Y olduğunda Z gerektirir"), konu etiketi değil.

## 4) Onay Özeti (kaydetmeden önce gösterilir)

Her not için, Türkçe, kısa:

```
📝 **Kaydedilecek not**
- **Başlık:** …
- **Kategori:** Geçici Not | Literatür Not | Zettelkasten
- **Etiketler:** A, B, C  (yeni: —)
- **Kaynak:** … (n kaynak) | —
- **Bağlantılar:** … | —
- **Tarih:** 2026-10-07
- **Gövde özeti:** 2–3 cümle
- **Bölümler:** Başlık 1 · Başlık 2 · Başlık 3

Onaylıyor musunuz? (evet / düzelt: …)
```

Gövdenin tam metni sohbete yazılmaz; kullanıcı notu Notion'da okur. Kullanıcı onaydan önce
belirli bir bölümü görmek isterse yalnızca o bölüm gösterilir.

Paket modunda üç not üst üste listelenir ve tek soru sorulur:
"Üç notu da bu haliyle kaydedeyim mi?"

Düzenleme modunda tablo kullanılır:

```
| # | Not | İşlem | Gerekçe |
|---|-----|-------|---------|
| 1 | Başlık | Etiket ekle: Yapay Zeka, Ai Agent | Gövde ajan mimarisini anlatıyor |
| 2 | Başlık | Kategori → Arşiv (şu an: Geçici Not) | Başlık ve gövde boş |

Tümünü uygulayayım mı? (evet / şu satırları çıkar: …)
```

## 5) Kayıt sonrası rapor

```
✅ Kaydedildi: **Başlık** (Kategori) — Etiketler: … — [Notion'da aç](URL)
```
