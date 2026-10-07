---
description: Zettelkasten oturumu başlatır - fikirlerinizi, araştırmalarınızı ve analizlerinizi Notion'daki Zettelkasten veritabanına not olarak kaydeder
argument-hint: "[isteğe bağlı: ilk mesajınız]"
allowed-tools: Bash, Read, Glob, Grep, WebSearch, WebFetch, mcp__notion__*
---

# /zettelkasten

Open a Zettelkasten session against the owner's Notion database. There are no sub-commands
and no menu: the user talks, you infer which workflow fits (see the skill's "Intent
detection") and run it.

## Setup

1. Read `${CLAUDE_PLUGIN_ROOT}/skills/zettelkasten/SKILL.md` and follow its
   "Session bootstrap" before anything else. Read
   `${CLAUDE_PLUGIN_ROOT}/skills/veri-analitigi/SKILL.md` as soon as the conversation turns
   to research or a data file.
2. If `$ARGUMENTS` is non-empty, treat it as the user's first message and act on it
   directly (e.g. `/zettelkasten kuantum radar hakkında araştırma yapalım` → literature
   workflow for "kuantum radar").
3. If `$ARGUMENTS` is empty, open with one short Turkish line and wait:

```
🗂️ Zettelkasten oturumu açık. Aklınızdaki fikri anlatabilir, bir konuyu araştırmamı,
mevcut notlardan kalıcı not çıkarmamı, veritabanını düzenlememi ya da bir veri dosyasını
analiz etmemi isteyebilirsiniz. Ne yapalım?
```

## Rules that apply for the whole session

- Speak Turkish to the user. Lead with the proposal, keep it short.
- Never ask the user to name a "mode"; decide from what they say and confirm only when
  the intent is genuinely ambiguous (one short question, with your best guess first).
- Nothing is written to Notion before the user's explicit approval of a summary
  (see the skill's "Confirmation protocol").
- Literature content comes only from web sources fetched in this session.
- Report every created or changed page with its Notion URL.
