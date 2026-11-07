# Weather Singularities: Mod Format and Rule Set

**API 1.2 · Documentation as at 7 November 2026 · Astronomical Clock 1.1.7.96**  
**Example dataset:** `de-gaxmann.json`, version 0.3.6.  
**Status:** Sections 1–5 describe the currently documented and supported interface. Section 6 records extensions that have already been designed but not yet implemented. Fields mentioned in Section 6 must not currently be assumed to be supported by the engine.

A mod file contains regional weather rules and their messages. The app reads these files from `mod/`. The build process generates `mod/index.json` from them, including the identifier, filename, translated mod names and areas. JSON is a data format, not executable code. All API keys are in English; user-defined event and variant keys must be reused in the language blocks. Metadata and rules precede `languages`.

## 1. Structure of a Mod File

The following complete structural example shows a single event. The supplied dataset `mod/de-gaxmann.json` contains nine event groups with a total of ten rules.

```json
{
  "api": "1.2",
  "id": "de-wettersingularitaeten",
  "version": "0.3.6",
  "areas": [
    {
      "bounds": {
        "lat_min": 47.2,
        "lat_max": 55.2,
        "lon_min": 5.7,
        "lon_max": 15.2
      }
    }
  ],
  "events": {
    "eisheilige": {
      "period": { "from": "05-10", "to": "05-27" },
      "event_anchor": "tmin",
      "search": [
        ["tmin.abs", "<=", 6],
        ["tmax.abs", "<=", 26],
        ["tmin.rel", "<=", -6.5]
      ],
      "display": ["tmax", "tmin"],
      "comment": ""
    }
  },
  "languages": {
    "de": {
      "mod_name": "Deutschland",
      "eisheilige": {
        "link": "https://de.wikipedia.org/wiki/Eisheilige",
        "short_text": "Eisheilige kommen",
        "long_text": "Zur Zeit der Eisheiligen kündigt sich ein Kälteeinbruch an."
      }
    },
    "en": {
      "mod_name": "Germany",
      "eisheilige": {
        "link": "https://de.wikipedia.org/wiki/Eisheilige",
        "short_text": "Ice Saints cold spell is approaching",
        "long_text": "A cold spell associated with the Ice Saints is approaching."
      }
    }
  }
}
```

`api` is a string identifying the interface version, while `version` identifies the version of the rule set. The technical `id` remains unchanged if the file is renamed or a new dataset version is released. `areas` contains one or more geographical rectangles in decimal degrees. The boundaries are inclusive; a match in any one rectangle is sufficient. Rectangles belonging to different mods may overlap. The German example uses an approximate geographical bounding box, not the exact national border.

An entry in `index.json` consists of `id`, `file`, `names` and `areas`. The names come from `languages.*.mod_name`.

## 2. Events, Variants and Time Windows

A simple event contains `period`, `event_anchor`, `search` and `display` directly under its key. A compound event such as `schafskaelte` instead contains named variants such as `frueh` and `spaet`. Each variant contains its own complete rule. There is no additional `variants` key, nor a redundant `period` or `display` entry at group level. The corresponding translations use the same keys.

| Item | Limit and behaviour |
|---|---|
| Events per JSON file | At most 32 entries at the top level of `events`, in file order. A group counts as one event. |
| Variants per event | At most 8. Larger groups are skipped. |
| Event period | At most 70 calendar days, including the start and end dates. Longer events and groups are skipped. |
| `short_text` | At most 80 Unicode characters; if exceeded, the first 79 characters are retained, followed by `…`. |
| `long_text` | At most 1024 Unicode characters; if exceeded, the first 1023 characters are retained, followed by `…`. |
| Displayed weather variables | The first 3 entries in `display`, each for 4 days starting today. |

`period.from` and `period.to` use `MM-DD`. Both the start and end dates are inclusive. If the end date falls before the start date in the calendar, the window ends in the following year. For a group, the period runs from the earliest variant start to the latest variant end, including the days between variants. The late-winter period ends on 28 February, including leap years. The relevant date is the local date at the location being considered.

The optional **`comment`** is a free-text field **for each event rule**. The author uses it to document the years actually examined and the percentage of years in which the detection rule was triggered at least once within the respective time window. The statistical statement should be verifiable, for example by specifying the years examined, the years with matches and the data source used. For compound events, `comment` belongs in each individual variant alongside its `period`, `search` and `display`, not at group level. The engine does not use this comment for selection, weather calculations or display. The field may remain empty until the analysis has been carried out.

```json
"comment": "Years examined: [years]; matches: [matching years]/[years examined] ([percentage] %); source: [data source]"
```

## 3. Rules and Event Date

A comparison has the form `[field, operator, numeric value]`. The permitted operators are `<`, `<=`, `>`, `>=`, `==` and `!=`. The outer list combines conditions with AND. Nested groups start with `"or"` or `"and"` and contain at least one condition. Multiple groups at the same level and recursive nesting are permitted. Empty groups and unknown fields are invalid. An interpreter evaluates the permitted conditions; `eval()` is not used.

```json
"search": [
  ["tmin.abs", "<=", 0],
  ["tmax.abs", "<=", 5],
  ["or",
    ["tmin.rel", "<=", -6],
    ["tmax.rel", "<=", -6]
  ]
]
```

Alternatively, a nested AND condition within OR is permitted:

```json
"search": [
  ["or",
    ["and", ["tmin.abs", "<=", 0], ["tmin.rel", "<=", -6]],
    ["and", ["tmax.abs", "<=", 5], ["tmax.rel", "<=", -6]]
  ]
]
```

| Supported field | Meaning | Unit |
|---|---|---|
| `tmin.abs` | Actual daily minimum temperature | °C |
| `tmax.abs` | Actual daily maximum temperature | °C |
| `tmin.rel` | Minimum temperature minus reference temperature | °C |
| `tmax.rel` | Maximum temperature minus reference temperature | °C |
| `precip` | Precipitation amount on the event date (multiplied with prob/100) | mm = l/m² |
| `prob` | Probability of precipitation on the event date | 0-100 % |

`.abs` refers to the actual temperature, not the absolute value of a difference. Negative `.rel` values indicate a decrease. The reference temperature is calculated by the PWA's weather analysis.

The first directional temperature condition in `search` determines whether the app looks for a decrease or an increase. A decrease requires a `.rel` comparison using `<` or `<=` with a negative threshold; an increase requires `>` or `>=` with a positive threshold.

`event_anchor` is mandatory and must be `"tmin"` or `"tmax"`. It determines which temperature match supplies the message date and must fall within `period`. `tmin.abs` and `tmin.rel` belong to the same minimum-temperature match, while `tmax.abs` and `tmax.rel` belong to the same maximum-temperature match. These two matches may occur on different days. Unshifted `precip` and `prob` conditions refer to the anchor date.

`search` identifies candidates. The optional `event_check` evaluates additional conditions for each candidate; if a check fails, further candidates may be examined. An example is the return of autumn warmth with `"event_anchor": "tmax"`:

```json
"event_check": [
  ["prob", "<", 70],
  ["precip", "<", 2]
]
```

If the same rule has several visible matches, the one with the largest absolute temperature change at the anchor is displayed; in the event of a tie, the earlier date is used. 

## 4. Messages, Translations and Display

For each event or variant, `short_text` and `long_text` form a pair. An optional HTTP or HTTPS `link` is placed at event level in the respective language block; variants and a `NONE` message use the same link. Language blocks use two-letter language codes (for example `de`, `en`, `pt`). The translation lookup starts with the selected language, followed by `en`, `de` and the remaining available language blocks in file order. Incomplete messages are skipped; the short and long texts always come from the same language block.

An optional `NONE` entry containing `short_text` and `long_text` generates a message after the entire event window has passed if it can be established that neither the event nor any variant occurred. This requires the complete period, including all variants, to have been checked against complete data. Missing historical data is not proof that an event did not occur. Without a `NONE` entry, no non-occurrence message is generated. The app must distinguish observed events from events that have only been forecast.

The data page displays matches as expandable short titles with a relative day and weekday, for example “Day after tomorrow (Sun): Ice Saints cold spell is approaching”. A table of values appears below the long text. The supported display variables are `tmax`, `tmin`, `precip` and `prob`; the temperature rows are labelled “Max:” and “Min:”. If precipitation occurs on the event date, it is displayed automatically, even when `precip` is not listed in `display`. It is therefore normally unnecessary to include `precip` in `display`.

## 5. Evaluation Limits and Regional Assignment

An event window may cover at most **70 calendar days**. Temperature changes also require the preceding seven reference days. Forecasts extend up to three days ahead; past matches remain visible for at most six local calendar days. `NONE` is evaluated no earlier than the day after the final day of the window and is also displayed for at most six days. No `NONE` may be generated for time windows that cannot be fully evaluated.

Regional assignment is a function of the PWA, not of the JSON rule set. The aim is to assign exactly one mod automatically to each location. The PWA settings provide the modes **Automatic** and **Off**. Regional prioritisation where rectangles overlap is described in [Regional mods and automatic selection](../docs/mod-Anleitung/wettersingularitaeten-regionalmods.md); the mathematical details have yet to be specified.

## 6. Planned: Extensions to the Field Language

The following components are planned. **They are not supported by the interpreter.** The engine should reject unknown or not yet implemented fields rather than silently evaluating them. Later implementation requires the outstanding specifications and corresponding tests.

### 6.1 Event-Related Temperature Fields

| Planned field | Meaning |
|---|---|
| `tevent.abs` | Actual temperature of the detected temperature event (`tmin` or `tmax`). |
| `tevent.rel` | Temperature change of the same temperature event. |

These fields are intended for `event_check` after `search` has found a temperature candidate.

```json
"event_check": [
  ["tevent.abs", "<=", 5],
  ["tevent.rel", "<=", -6]
]
```

`tevent.type` will not be introduced for the time being.

### 6.2 Multi-Day Weather Conditions

The planned field `precip|days:N` denotes **N consecutive days**, on each of which the individual daily value must satisfy the comparison. It is not a sum over N days. For example, `precip|days:3` with `>= 8` means at least 8 l/m² on each of the three days:

```json
"search": [
  ["precip|days:3", ">=", 8]
]
```

Further field families of the form `field|days:N` are planned only once the engine supplies the relevant weather variable and the required daily data. **Still to be specified:** Which day of a detected multi-day sequence counts as the event date, and which date additional `event_check` conditions refer to. The example therefore does not yet represent a commitment to executable support.

### 6.3 Time Offsets for `event_check`

Time references are intended to be explicit and unambiguous. Without a suffix, the event date applies. `|event:N` denotes an offset from the event date; `|day:N` denotes an offset from today's local date at the location:

```json
"event_check": [
  ["prob", "<", 8],
  ["precip|event:1", ">=", 8],
  ["precip|event:-1", ">=", 8],
  ["precip|day:0", ">=", 8]
]
```

`precip|event:1` means the day after the event, while `precip|event:-1` means the day before it; `precip|day:0` means today and `precip|day:1` means tomorrow. Forms such as `precip|-1` are not part of the documented format. If a required daily value is missing, the condition cannot be evaluated; it is not automatically false.

### 6.4 Additional Display Variables and Open Questions

Additional variables such as `clarity` are planned for `display`. Their presentation and daily data basis have not yet been defined; the supported variables are `tmax`, `tmin`, `precip` and `prob`.

Before the extended fields are released, the reference date for multi-day sequences, permitted offsets, data availability and the integration of up to seven additional reference days into the history must, in particular, be specified and tested.

The planned regional assignment, publication via GitHub and the simple test interface are covered in [Regional mods and automatic selection](../docs/mod-Anleitung/wettersingularitaeten-regionalmods.md). The current implementation status of the PWA is described under [Implementation](../docs/mod-Anleitung/wettersingularitaeten-implementierung.md).
