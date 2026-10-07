---
description: Zettelkasten oturumu başlatır - geçici not, literatür notu, kalıcı not, paket, beyin fırtınası, düzenleme veya veri analizi
argument-hint: "[gecici | literatur | kalici | paket | beyin-firtinasi | duzenle | analiz] [konu]"
allowed-tools: Bash, Read, Glob, Grep, WebSearch, WebFetch, mcp__notion__*
---

# /zettelkasten

Start a Zettelkasten session against the owner's Notion database.

## Setup

1. Read `${CLAUDE_PLUGIN_ROOT}/skills/zettelkasten/SKILL.md` and follow its
   "Session bootstrap" before anything else. For modes `literatur`, `paket` and `analiz`
   also read `${CLAUDE_PLUGIN_ROOT}/skills/veri-analitigi/SKILL.md`.
2. Parse `$ARGUMENTS`:
   - First token is the mode if it is one of
     `gecici`, `literatur`, `kalici`, `paket`, `beyin-firtinasi`, `duzenle`, `analiz`
     (accept Turkish characters and common variants: `geçici`, `literatür`, `kalıcı`,
     `beyin`, `düzenle`, `organize`, `analiz`, `veri`).
   - The rest is the topic / idea / file path; pass it into the mode.
3. If no mode is given, show this menu in Turkish and wait for the user's choice:

```
🗂️ Zettelkasten — ne yapmak istersiniz?
1. Geçici not oluştur (aklınızdaki fikri yapılandırıp kaydedelim)
2. Literatür notu oluştur (web'de kaynaklı araştırma → not)
3. Kalıcı not oluştur (mevcut notlardan Zettelkasten notu)
4. Zettelkasten paketi (1 → 2 → 3 uçtan uca, tek onay)
5. Beyin fırtınası (fikri birlikte geliştirelim)
6. Düzenleme ve organizasyon (etiket, şablon, arşiv)
7. Veri analizi (CSV/Excel dosyasını analiz edip not olarak kaydedelim)
```

## Rules that apply in every mode

- Speak Turkish to the user. Lead with the proposal, keep it short.
- Nothing is written to Notion before the user's explicit approval of a summary
  (see the skill's "Confirmation protocol").
- Literature content comes only from web sources fetched in this session.
- Report every created or changed page with its Notion URL.
