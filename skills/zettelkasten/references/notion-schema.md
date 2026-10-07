# Notion şeması — "Zettelkasten Veritabanı"

Bu dosya modele yöneliktir; kullanıcıya gösterilmez.

## Kimlikler

| Nesne | Kimlik / URL |
|---|---|
| Üst sayfa "Zettelkasten" | `https://app.notion.com/p/3dad524b926f8099ac94cc786e50ee9a` (page_id `3dad524b926f8099ac94cc786e50ee9a`) |
| Veritabanı | `https://app.notion.com/p/3dad524b926f801ebd45c7fe0252b11d` |
| Veri kaynağı (yazma hedefi) | `collection://3dad524b-926f-8016-b73f-000b8d778e7c` |

`notion-create-pages` için parent:

```json
{ "type": "data_source_id", "data_source_id": "3dad524b-926f-8016-b73f-000b8d778e7c" }
```

## Özellikler (properties)

| Özellik | Tür | SQL sütunu | Not |
|---|---|---|---|
| `Name` | title | `"Name"` | Başlık. Düz metin. |
| `Kategori` | select | `"Kategori"` | `Geçici Not` · `Literatür Not` · `Zettelkasten` · `Arşiv` (yalnızca arşivleme) |
| `Etiket` | multi_select | `"Etiket"` (JSON dizi) | Aşağıdaki listeden; yeni etiket onayla. |
| `Kaynak` | text (rich) | `"Kaynak"` | Numaralı liste; satırlar `\n` ile ayrılır. |
| `Bağlantılar` | text (rich) | `"Bağlantılar"` | `<mention-page>` listesi. |
| `Tarih` | date | `"date:Tarih:start"`, `"date:Tarih:end"`, `"date:Tarih:is_datetime"` | Yazarken `date:Tarih:start` + `date:Tarih:is_datetime: 0`. |

Sistem sütunları: `url`, `createdTime`.

### Örnek: sayfa oluşturma yükü

```json
{
  "parent": { "type": "data_source_id", "data_source_id": "3dad524b-926f-8016-b73f-000b8d778e7c" },
  "pages": [{
    "properties": {
      "Name": "Görsel hiyerarşi Gestalt ilkelerine dayanır",
      "Kategori": "Literatür Not",
      "Etiket": ["Grafik Tasarım"],
      "Kaynak": "1. Figma - Görsel Hiyerarşi Nedir? - https://www.figma.com/resource-library/what-is-visual-hierarchy/\n2. NN/g - Visual Hierarchy - https://www.nngroup.com/articles/visual-hierarchy-ux-definition/",
      "Bağlantılar": "<mention-page url=\"https://app.notion.com/p/3e9d524b926f808bac75ef493af62c13\"/>",
      "date:Tarih:start": "2026-10-07",
      "date:Tarih:is_datetime": 0
    },
    "content": "## Tanım\nGörsel hiyerarşi, öğeleri önem sırasına göre düzenleme pratiğidir. \\[1\\]\n..."
  }]
}
```

### Örnek: sorgular (SQL modu)

Tablo adı veri kaynağı URL'sidir; her zaman çift tırnak içinde yazılır.

```sql
-- Başlıkta anahtar kelime (kopya kontrolü; arşiv hariç)
SELECT url, "Name", "Kategori", "date:Tarih:start"
FROM "collection://3dad524b-926f-8016-b73f-000b8d778e7c"
WHERE "Name" LIKE ? COLLATE NOCASE
  AND ("Kategori" IS NULL OR "Kategori" <> 'Arşiv');   -- params: ["%makyavel%"]

-- Kategoriye göre son notlar
SELECT url, "Name", "Etiket", "Kaynak"
FROM "collection://3dad524b-926f-8016-b73f-000b8d778e7c"
WHERE "Kategori" = ? ORDER BY createdTime DESC LIMIT 20;   -- params: ["Literatür Not"]

-- Etiketi boş satırlar (düzenleme modu)
SELECT url, "Name", "Kategori"
FROM "collection://3dad524b-926f-8016-b73f-000b8d778e7c"
WHERE "Etiket" IS NULL OR "Etiket" = '[]';

-- Belirli bir etiketi taşıyanlar
SELECT url, "Name" FROM "collection://3dad524b-926f-8016-b73f-000b8d778e7c"
WHERE "Etiket" LIKE ?;                          -- params: ["%\"Veri Bilimi\"%"]

-- Aynı başlıklı satırlar (kopya adayları; arşiv hariç)
SELECT "Name", COUNT(*) AS n FROM "collection://3dad524b-926f-8016-b73f-000b8d778e7c"
WHERE "Kategori" IS NULL OR "Kategori" <> 'Arşiv'
GROUP BY "Name" HAVING n > 1;

-- Arşivdekiler
SELECT url, "Name" FROM "collection://3dad524b-926f-8016-b73f-000b8d778e7c"
WHERE "Kategori" = 'Arşiv';
```

Zengin metni (mention'lar) bozmadan okumak için `mode: "rows"` kullan; SQL çıktısı
mention'ları düz metne çevirebilir.

## Mevcut etiketler (2026-10-07 itibarıyla, 77 adet)

Canlı liste `notion-fetch` ile alınan şema ile çelişirse canlı liste geçerlidir.

Girişimcilik · Grafik Tasarım · Bilgisayar Destekli Tasarım · 3D Printer · Ekonomi · Youtube ·
Politika & Siyaset · Askeri · Teknoloji · Uzay · Uydu Teknolojisi · Telefon · Teknoloji Tasarım ·
Konsept · Bilişim · Strateji · Program · Polis · Yapay Zeka · Ar-Ge · Blok Zincir · Kripto Para ·
Kuantum Bilgisayar · Nükleer Enerji · Futurism · İşletme · Ai Agent · Veri Bilimi · Felsefe ·
İstihbarat · SIGINT · Metod · Drone · Robotik · Gözetim · Distopya · Propaganda · Manipülasyon ·
Prodüksiyon · Algoritma · Yazılım_Mühendisliği · Optimizasyon · Donanım · Edge Computing ·
Biyoloji · Farmakoloji · Süper Bilgisayar · OSINT · Kamu & Devlet · Generative Brief ·
Proje Yönetimi · Endüstriyel Tasarım · Enerji · İnovasyon · Proje · Markalaşma ·
Beyin Bilgisayar Arayüzü · Biyoteknoloji · Transhumanizm · Medya · Dijital İkiz · Simülasyon ·
Psikoloji & Psikiyatri · Nükleer Silah · Dijital Silah · Sosyoloji · Kişisel Gelişim ·
Sistem Mühendisliği · Portföy · Uluslararası İlişkiler · Analiz · Uzay_Madenciliği ·
Genetik Bilimi · Kuantum Fiziği · Pragmatizm · Vaka Çalışması

Etiket seçerken: önce konu alanı (örn. `Yapay Zeka`), sonra alt alan (örn. `Ai Agent`),
gerekiyorsa tür (`Metod`, `Konsept`, `Analiz`, `Vaka Çalışması`, `Proje`). En fazla 5.

## Notion-flavored Markdown — kullanılan alt küme

- Başlıklar: `## Başlık`, `### Alt başlık` (sayfa başlığı gövdeye yazılmaz).
- Vurgu: `**kalın**`, `*italik*`. Kod: `` `kod` ``.
- Listeler: `- madde`, `1. madde`; alt öğeler **tab** ile girintilenir.
- Boş satır: yalnızca `<empty-block/>` (kendi satırında). Düz boş satırlar silinir.
- Alıntı: `> metin`. Çok satırlı alıntıda satırlar `<br>` ile ayrılır.
- Ayraç: `---`. Callout: `<callout icon="💡">\n\tmetin\n</callout>`.
- Tablo: `<table header-row="true"><tr><td>..</td></tr></table>` (hücrelerde yalnızca zengin metin).
- Görsel: `![Açıklama](URL)`; yüklenen dosya için `create-file-upload` yanıtındaki
  `suggested_markdown` aynen kullanılır.
- Sayfa mention: `<mention-page url="https://app.notion.com/p/<id>"/>` — mevcut sayfaya
  referans. **`<page url=...>` asla kullanılmaz** (sayfayı taşır).
- Kaçış: `\ * ~ \` $ [ ] < > { } | ^` karakterleri gövdede `\` ile kaçırılır; mevcut notlar
  atıfları `\[1\]` biçiminde tutar.
- Kod bloğu içinde kaçış yapılmaz.

## Araç haritası

| İş | Araç |
|---|---|
| Şema / sayfa okuma | `notion-fetch` |
| Satır sorgulama | `notion-query-data-sources` (`mode: sql` veya `rows`) |
| Başlıkla arama | `notion-search` (`data_source_url` ile daraltılabilir) |
| Sayfa oluşturma | `notion-create-pages` |
| Özellik / içerik güncelleme | `notion-update-page` (`update_properties`, `update_content`, `insert_content`) |
| Arşivleme | `notion-update-page` → `update_properties` → `{"Kategori": "Arşiv"}` |
| Görsel yükleme | `notion-create-file-upload` → `curl` ile POST → `suggested_markdown` |
