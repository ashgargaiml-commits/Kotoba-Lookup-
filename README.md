# ことば lookup — offline Japanese vocabulary tool

A single-file, fully offline Japanese vocabulary lookup tool for iPhone (Safari).
Search an English word, get the hiragana, live-computed romaji, kanji, and
optional audio playback — no network required after the first save.

## Features

- **24,000+ word dictionary**, built entirely offline once saved to your device
- **Search by English meaning**, with ranked results (exact word match ranks
  above partial/substring matches, so short queries don't return unrelated
  false positives)
- **Kanji + hiragana + auto-computed romaji** for every entry — romaji is
  generated live from hiragana via a Hepburn conversion table, not stored
  per-word
- **JLPT level tags** (N5–N1) where available
- **Voice output**: taps the device's Japanese text-to-speech voice, if one
  is installed
- **Voice input**: speak the English word instead of typing (`webkitSpeechRecognition`)
  — requires network and mic permission at the moment of use, since on-device
  speech recognition isn't available in mobile browsers
- **"+ Add word"**: save your own words directly on-device (IndexedDB), no
  server, no account, works offline immediately

## How it works

Everything lives in a single `.html` file with the dictionary embedded as a
JSON array. There's no backend, no build step, and no external requests once
the file is opened. Save it to Files on your phone and open it directly in
Safari (or add it to your home screen) — after that first open, it works with
airplane mode on for lookup, romaji, and audio playback. Voice *input* is the
one feature that needs a live connection, since speech-to-text in mobile
browsers is cloud-based rather than on-device.

Words added through "+ Add word" are stored in the browser's IndexedDB, scoped
to that specific saved file. They do not carry over automatically if you
download a fresh copy of this file later.

## Data sources & attribution

This tool bundles vocabulary from two sources, merged and deduplicated:

1. **JLPT N5–N1 vocabulary** (~8,000 words) — from
   [jamsinclair/open-anki-jlpt-decks](https://github.com/jamsinclair/open-anki-jlpt-decks),
   originally sourced from [tanos.co.uk](http://www.tanos.co.uk/jlpt/) and
   [chyyran/jlpt-anki-decks](https://github.com/chyyran/jlpt-anki-decks).
2. **JMdict (common-only edition)** (~16,000 additional words) — from
   [JMdict-simplified](https://github.com/scriptin/jmdict-simplified), a JSON
   distribution of the [JMdict project](https://www.edrdg.org/jmdict/j_jmdict.html).
   JMdict is property of the Electronic Dictionary Research and Development
   Group (EDRDG) and is used here under the terms of their
   [Creative Commons Attribution-ShareAlike Licence (V4.0)](https://www.edrdg.org/edrdg/licence.html).

If you redistribute this repo, keep this attribution section — it's a
condition of the JMdict license, not just courtesy.

## Known limitations

- **Not a complete dictionary.** ~24,000 words covers common daily and JLPT
  vocabulary, not the full ~200,000-entry JMdict corpus. Business jargon,
  technical terms, and slang are inconsistently covered.
- **English-gloss search only.** No Japanese-to-English direction, no kanji
  input search, no conjugation handling (verbs are dictionary form only).
- **Voice input reliability is device-dependent.** iOS Safari's support for
  `webkitSpeechRecognition` isn't consistent across versions; test before
  relying on it.
- **Voice output requires a Japanese voice pack** to already be installed on
  the device; the tool detects and reports this rather than failing silently.
- **No sync.** Words added via "+ Add word" live only in that browser's
  IndexedDB for that specific file — there's no export/import or cloud sync
  yet.

## Possible next steps

- Export/import for user-added words, so they survive re-downloading the file
- Example sentences (JMdict has a separate examples-linked release)
- Kanji stroke order / writing practice
- Katakana-only loanword handling improvements

## License

The dictionary data retains its original licenses (see Attribution above) —
this applies regardless of the license below.

The code in this repository (the HTML/JS tool itself) is licensed under the
MIT License. See [LICENSE](LICENSE) for the full text.
