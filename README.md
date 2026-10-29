# Voice Mode keyboard dictionaries

Word lists the Voice Mode keyboards download when someone adds a typing language: suggestions,
autocorrect, next-word prediction and spell check. Also the one small model file that exists nowhere
else (Smart Turn). Only data lives here, no app code.

| Folder | What | Used by |
| --- | --- | --- |
| `glide-dicts-v1/` | One word list per language (`<lang>.json`, word → how common) | Android |
| `bigram-dicts-v1/` | Word pairs per language, for next-word guesses | Android |
| `trigram-dicts-v1/` | Word triples per language, for next-word guesses | Android |
| `language-packs-v1/` | Chinese pinyin table | Android |
| `ios-dicts-v1/` | The same word lists in the iPhone keyboard's format | iPhone |
| `whisper-models-v1/` | Smart Turn v3.2 (decides whether a spoken thought is finished, for long dictations) | Android |

The apps download from `https://raw.githubusercontent.com/alvanx/voice-mode-dictionaries/main/<folder>/<file>`
and check each file's exact size and SHA-256 fingerprint, which are written into the app.

## The one rule: never change or delete a published file

Phones in the wild check every file against the fingerprint their app version knows. A changed file
fails that check, gets thrown away and downloaded again, over and over. So:

- A rebuilt list gets a **new file name** (for example `pl.v2.json`, `de_bigrams_150k.txt`), or a new
  folder (`-v2`). Then the app's list is updated to the new name.
- Old files stay, for the app versions that still ask for them.

## Where the files come from

Copied from Dictate Keyboard's releases (Apache 2.0). Sources and licences of the words: `NOTICE` and
`attribution/`. The tools that build the lists live in the Android app's repository
(`tools/glide-dict/`, `tools/pinyin-dict/`) and, for the iPhone format, in the iPhone app's
(`tools/import_android_dicts.py`).
