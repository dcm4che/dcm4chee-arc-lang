## Resources for providing different languages for the Web UI of dcm4chee-arc-light

There are two different types of language specific resources:
- a key/value map in JSON format used by the UI for labeling UI components, and
- various [JSON Schema](https://json-schema.org/) files, specifying the name, type, description, default value
  of configuration attributes of various configuration entities.

First are located under `src/main/webapp/asserts/##.json`, with `##` as the
[ISO 639-1 two-letter code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) of the language
(e.g. `es` for Spain, `pt` for Portuguese, `ru` for Russian). 

The second are located under `src/main/webapp/asserts/schema/`. For other languages then English, a
subdirectory  with the [ISO 639-1 two-letter code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) of the
language has to be created, including copies of that JSON Schema files with translated values for
`"title"` and `"description"` JSON properties.

Alternatively to directly editing that JSON files, you may translate `title` and `description` columns in
corresponding CSV files, located in `src/csv`, and committing the modified files under a subdirectory named with
the [ISO 639-1 two-letter code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) of the language.

The English version of the CSV files are created/updated from the JSON Schema files by invoking dcm4che's utility
[json2csv](https://github.com/dcm4che/dcm4che/tree/master/dcm4che-tool/dcm4che-tool-json2csv):
```
$ json2csv src/main/webapp/assets/schema src/csv
src/main/webapp/assets/schema/hl7ExportRule.schema.json=>src/csv/hl7ExportRule.schema.csv
src/main/webapp/assets/schema/hl7OrderScheduledStation.schema.json=>src/csv/hl7OrderScheduledStation.schema.csv
...
src/main/webapp/assets/schema/metrics.schema.json=>src/csv/metrics.schema.csv
```

Translated versions of the CSV files for one language can be converted back to JSON Schema files by invoking (e.g.)
```
$ json2csv src/main/webapp/assets/schema src/csv/hi src/main/webapp/assets/schema/hi
src/csv/hi/hl7ExportRule.schema.csv=>src/main/webapp/assets/schema/hi/hl7ExportRule.schema.json
src/csv/hi/hl7OrderScheduledStation.schema.csv=>src/main/webapp/assets/schema/hi/hl7OrderScheduledStation.schema.json
...
src/csv/hi/metrics.schema.csv=>src/main/webapp/assets/schema/hi/metrics.schema.json
```

If the translated CSV files miss some (new) entries already defined in the English version of the JSON Schema files
in `src/main/webapp/assets/schema`, the created language specific JSON Schema file are supplemented with the entries
from the English version. Converting the so created JSON Schema files back to the language specific CSV files by
invoking (e.g.) 
```
$ json2csv src/main/webapp/assets/schema/hi src/csv/hi
src/main/webapp/assets/schema/hi/hl7ExportRule.schema.json=>src/csv/hi/hl7ExportRule.schema.csv
src/main/webapp/assets/schema/hi/hl7OrderScheduledStation.schema.json=>src/csv/hi/hl7OrderScheduledStation.schema.csv
:
src/main/webapp/assets/schema/hi/metrics.schema.json=>src/csv/hi/metrics.schema.csv
```
will add the previous missing entries in the CSV files, were they can be replaced by translated values for `title`
and `description`.
