## Resources for providing different languages for the Web UI of dcm4chee-arc-light

### Schemas 

Defines configuration attribute names and descriptions

To add an additional language
1. Create a sub-directory in directory `schema` with the
[ISO 639-1 two-letter code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) of the language as name
(e.g. `es` for Spain, `pt` for Portuguese, `ru` for Russian)
2. Copy all CVS files from the `schema` to the created sub-directory
3. Replace the title and description fields by the translated terms in the copied files
