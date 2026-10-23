# WotLK 3.3.5a Language Merge

WoW 3.3.5a ties text and audio to the same locale MPQs. Renaming German speech MPQs to enUS works for most content, but dungeon speech (Brann in Halls of Stone, etc.) is stored with highest priority in the patch-enUS*.mpq files, not in the speech MPQs. Those patch MPQs also contain the English text tables (Spell.dbc, Item.dbc, etc.), so replacing them entirely would switch the text to German too.

This repo contains merged locale sets that keep one language for text and the other for audio.

## Folders

- `enus/` - original English locale MPQs
- `dede/` - original German locale MPQs
- `enDE/` - English text, German audio (for `locale="enUS"` clients)
- `deEN/` - German text, English audio (for `locale="deDE"` clients)

## Usage

English text + German audio (enDE):
1. Set `SET locale="enUS"` in `WTF/Config.wtf`.
2. Copy all files from `enDE/` into `Data\enUS\`, overwriting existing files.

German text + English audio (deEN):
1. Set `SET locale="deDE"` in `WTF/Config.wtf`.
2. Copy all files from `deEN/` into `Data\deDE\`, overwriting existing files.

Delete the `Cache` folder after copying.

## How it was done

1. Copied the base locale MPQs from the source language (locale, expansion-locale, lichking-locale).
2. Replaced the `*-speech-*.mpq` files with the target language's versions (renamed to match the locale).
3. Extracted all `Sound/` files from the target language's `patch-*.mpq` files and rebuilt the source language's `patch-*.mpq` files from scratch with those sound files injected. This overwrites only the audio while leaving all DBC text tables untouched.

## Notes

- The `patch-*.mpq` files in the merged folders contain both the original text tables and the injected audio files. Do not replace them with the originals.
