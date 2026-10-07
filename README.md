# Claude-Plugin-Zettelkasten

Veri analitiği alanında uzmanlaştırılmış bu Claude Code plugin'i, kullanıcıdan gelen direktifler doğrultusunda analitik çalışmalar gerçekleştirir ve çalışma sonuçlarını **Zettelkasten** formatında **Notion veritabanına** kaydeder.

> Bu plugin yalnızca kişisel kullanım içindir: sahibinin Notion veritabanına sabitlenmiştir ve dağıtım/kurulum için paketlenmemiştir.

## İçerik

```
.claude-plugin/
  plugin.json            # Plugin manifesti
.mcp.json                # Notion MCP bağlantısı (https://mcp.notion.com/mcp)
commands/
  zettelkasten.md        # /zettelkasten komutu (tek komut + alt modlar)
skills/
  zettelkasten/
    SKILL.md             # Not türleri, akışlar, onay protokolü, katı kurallar
    references/
      notion-schema.md   # Veritabanı kimlikleri, özellikler, SQL sorguları, etiket listesi, Markdown
      templates.md       # Geçici / Literatür / Zettelkasten not şablonları, onay özeti
  veri-analitigi/
    SKILL.md             # Araştırma + veri analizi ortak kuralları
    references/
      research.md        # Web araştırma yöntemi, kaynak güvenilirliği, atıf biçimi
      data-analysis.md   # CSV/Excel analizi, grafik üretimi, Notion'a görsel yükleme
```

### Claude Skills
- **Zettelkasten:** Uygulamanın asıl değer önerisi. Modele Zettelkasten yöntemi, Notion şeması ve onay akışları konusunda rehberlik eder.
- **Veri Analitiği:** Modelin araştırma (web, kaynaklı), işleme, analiz ve görselleştirme becerilerini yönlendirir.

### Connectors
- **Notion MCP:** Kullanıcının çalışma alanına bağlanmak için `.mcp.json` üzerinden Notion'un resmi uzak MCP sunucusu kullanılır. İlk kullanımda `/mcp` ile **notion** sunucusuna yetki verilir.

## Notion Veritabanı

Tek veritabanı: **Zettelkasten Veritabanı** (üst sayfa: *Zettelkasten*).

| Özellik | Tür | Kullanım |
|---|---|---|
| Name | Başlık | İçeriğe göre düz metin başlık |
| Kategori | Select | `Geçici Not` · `Literatür Not` · `Zettelkasten` · `Arşiv` (arşivlenen notlar) |
| Etiket | Multi-select | Mevcut etiketlerden seçilir; yeni etiket için onay istenir |
| Kaynak | Metin | Literatür: `1. Başlık - URL` listesi · Zettelkasten: kaynak notların mention listesi |
| Bağlantılar | Metin | İlgili notların mention'ları |
| Tarih | Tarih | Notun oluşturulduğu gün |

## Kullanım Kılavuzu

Tek komut: `/zettelkasten [mod] [konu]`. Mod verilmezse menü gösterilir.

| Mod | Ne yapar |
|---|---|
| `gecici` | Aklınızdaki fikri yapılandırır, özet gösterir, onayla **Geçici Not** olarak kaydeder |
| `literatur` | Web'de (önce Türkçe, sonra İngilizce) 3–5 kaynaklı araştırma yapar; tek notta sentezler, `[n]` atıflarla **Literatür Not** olarak kaydeder |
| `kalici` | Mevcut geçici/literatür notlarından tek fikirli, atıflı, bağlantılı **Zettelkasten** notu üretir |
| `paket` | Geçici → literatür → kalıcı notu tek oturumda, tek toplu onayla üretip bağlar |
| `beyin-firtinasi` | Fikri birlikte geliştirir; isterseniz geçici not olarak kaydeder |
| `duzenle` | Etiket atama, şablona uygun hale getirme, fazlalık notları arşivleme (Kategori → `Arşiv`, toplu onay) |
| `analiz` | CSV/Excel dosyasını Python ile analiz eder, grafikleri Notion'a yükler, **Literatür Not** olarak kaydeder |

**NOT:** Bu fonksiyonlar bir paket halinde tek oturumda kullanılabileceği gibi ayrı ayrı da kullanılabilir.

### Temel kurallar
- Hiçbir not, özet gösterilip **açık onay** alınmadan Notion'a yazılmaz.
- Literatür notlarında kaynak zorunludur; model eğitim verisi kaynak olarak kullanılmaz.
- Plugin not silmez; "silme" işlemi notun kategorisini `Arşiv` yapmaktır (Notion'dan kalıcı silme kullanıcıya bırakılır).
- Veritabanı şeması plugin tarafından değiştirilmez.

## Sürüm Geçmişi
Mevcut Sürüm: v1.0
