## Resources for providing different languages for the Web UI of dcm4chee-arc-light

### `src/main/webapp/asserts/*.json` 

Defines text for UI elements beside configuration attribute names and descriptions

To add an additional language
1. Copy `src/main/webapp/asserts/en.json` to `src/main/webapp/asserts/##.json`, with `##` is the
[ISO 639-1 two-letter code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) of the language
(e.g. `es` for Spain, `pt` for Portuguese, `ru` for Russian), and replace string values on the right
by translated terms.

### `src/csv/*.csv` 

Defines configuration attribute names and descriptions

To add an additional language
1. Create a sub-directory in directory `src/csv` with the
[ISO 639-1 two-letter code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) of the language as name.
2. Copy all CSV files from the `src/csv` to the created sub-directory.
3. Replace the title and description fields by the translated terms in the copied files.
