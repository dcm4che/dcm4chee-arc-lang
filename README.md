## Resources for providing different languages for the Web UI of dcm4chee-arc-light

There are two different types of language specific resources:
- a key/value map in JSON format used by the UI for labeling UI components, and
- various [JSON Schema](https://json-schema.org/) files, specifying the name, type, description, default value
  of configuration attributes of various configuration entities.

First are located under `src/main/webapp/##.json`, second under `src/main/webapp/##/assets/schema/`,
with `##` as the [ISO 639-1 two-letter code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)
of the language (e.g. `es` for Spain, `pt` for Portuguese, `ru` for Russian). 

For adding support of an additional language, copy `src/main/webapp/en.json` to `src/main/webapp/##.json`,
with `##` as the [ISO 639-1 two-letter code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) of the new
language and replace the English property values by their translations.

Create a new directory `src/main/webapp/##/assets/schema/` and copy the JSON Schema files from `src/main/webapp/en/assets/schema/`
to the new directory and replace the English values for `"title"` and `"description"` JSON properties.

Alternatively to directly editing JSON Schema files, you may translate title and description separated by `|` in
corresponding key/value properties files, located in `src/props`, and committing the modified files under a
subdirectory named with the [ISO 639-1 two-letter code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)
of the language:

1. The English version of the key/value properties files are created/updated from the JSON Schema files by invoking
dcm4che's utility [json2props](https://github.com/dcm4che/dcm4che/tree/master/dcm4che-tool/dcm4che-tool-json2props):
   ```
   $ json2props src/main/webapp/en/assets/schema src/props/en
   src/main/webapp/en/assets/schema/hl7ExportRule.schema.json=>src/props/en/hl7ExportRule.props
   src/main/webapp/en/aassets/schema/hl7OrderScheduledStation.schema.json=>src/props/en/hl7OrderScheduledStation.props
   ...
   src/main/webapp/assets/en/schema/metrics.schema.json=>src/props/en/metrics.props
   ```

2. Translated versions of the key/value properties files for one language can be converted back to JSON Schema files by
invoking (e.g.)
   ```
   $ json2props src/main/webapp/en/assets/schema src/props/hi src/main/webapp/hi/assets/schema
   src/props/hi/hl7ExportRule.props=>src/main/webapp/hi/assets/schema/hl7ExportRule.schema.json
   src/props/hi/hl7OrderScheduledStation.props=>src/main/webapp/hi/assets/schema/hl7OrderScheduledStation.schema.json
   ...
   src/props/hi/metrics.props=>src/main/webapp/hi/assets/schema/metrics.schema.json
   ```
   
   If the translated key/value properties files miss some (new) entries already defined in the English version of the
   JSON Schema files in `src/main/webapp/en/assets/schema`, the created language specific JSON Schema file are supplemented
   with the entries from the English version.

3. Converting the so created JSON Schema files back to the language specific key/value properties files by invoking (e.g.) 
   ```
   $ json2props src/main/webapp/hi/assets/schema src/props/hi
   src/main/webapp/hi/assets/schema/hl7ExportRule.schema.json=>src/props/hi/hl7ExportRule.props
   src/main/webapp/hi/assets/schema/hl7OrderScheduledStation.schema.json=>src/props/hi/hl7OrderScheduledStation.props
   :
   src/main/webapp/hi/assets/schema/metrics.schema.json=>src/props/hi/metrics.props
   ```
   will add the previous missing entries in the key/value properties files, where title and description in English
   separated by `|` can be replaced by translated terms.

4. After the replacement of the supplemented new properties, the language specific JSON Schema files can be updated with
the new translated terms by converting the updated key/value properties files back to JSON Schema files as described in 2..
    

