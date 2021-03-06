# AutryMakers_Sheet1

## Add Column

## Add Node/Literal

## PyTransforms
#### _ObjectURI_
From column: _ObjectID_
``` python
return UM.uri_from_fields("object/", getValue("ObjectID"))
```

#### _MakerCopy_
From column: _Maker_
``` python
return getValue("Maker")
```

#### _PreferredTermsURI_
From column: _MakerCopy_
``` python
if getValue("Maker"):
    return "aat:300404670"
else:
    return ''
```

#### _BirthYear_
From column: _Dates_
``` python
time = getValue("Dates").replace(' ', '').lower()
dash_index = time.find('-')

if (time == 'NULL') or ('founded' in time) or ('circa' in time) or ('active' in time) or ('established' in time):
    return ''

if 'born' in time:
    born_index = time.find('born')
    return time[born_index + 4: born_index + 9]

if dash_index != -1:
    return time[dash_index-4:dash_index]

return ''
```

#### _DeathYear_
From column: _Dates_
``` python
time = getValue("Dates").replace(' ', '').lower()
dash_index = time.find('-')

if (time == 'NULL') or ('founded' in time) or ('circa' in time) or ('active' in time) or ('established' in time) or ('born' in time):
    return ''

if dash_index != -1:
    return time[dash_index+1:dash_index+5]

return ''
```

#### _MakerURI_
From column: _Maker_
``` python
if getValue("Maker") != 'NULL':
    return  UM.uri_from_fields("maker/", getValue("Maker"))
else:
    return ''
```

#### _MakerAppellationURI_
From column: _MakerURI_
``` python
if getValue("MakerURI") != 'NULL':
    return getValue("MakerURI") + "/appellation"
else:
    return ''
```

#### _ProductionURI_
From column: _ObjectURI_
``` python
return getValue("ObjectURI") + "/production"
```

#### _BirthURI_
From column: _BirthYear_
``` python
if getValue("BirthYear") != 'NULL':
    return getValue("MakerURI") + "/birth_event"
else:
    return ''
```

#### _BirthTimespanURI_
From column: _BirthYear_
``` python
if getValue("BirthYear") != 'NULL':
    return getValue("MakerURI") + "/birth_timespan"
else:
    return ''
```

#### _DeathURI_
From column: _DeathYear_
``` python
if getValue("DeathYear") != 'NULL':
    return getValue("MakerURI") + "/death_event"
else:
    return ''
```

#### _DeathTimespanURI_
From column: _DeathYear_
``` python
if getValue("DeathYear") != 'NULL':
    return getValue("MakerURI") + "/death_timespan"
else:
    return ''
```

#### _AutryMakerURLCopy_
From column: _AutryMakerURL_
``` python
return getValue("AutryMakerURL")
```

#### _LatestDeathDate_
From column: _DeathYear_
``` python
if getValue("DeathYear") != '':
    return "12-31-" + getValue("DeathYear")
else:
    return ''
```

#### _EarliestDeathDate_
From column: _DeathYear_
``` python
if getValue("DeathYear") != '':
    return "1-1-" + getValue("DeathYear")
else:
    return ''
```

#### _LatestBirthYear_
From column: _BirthYear_
``` python
if getValue("BirthYear") != '':
    return "12-31-" + getValue("BirthYear")
else:
    return ''
```

#### _EarliestBirthYear_
From column: _BirthYear_
``` python
if getValue("BirthYear") != '':
    return "1-1-" + getValue("BirthYear")
else:
    return ''
```

#### _NationalityAAT_
From column: _Nationality_
``` python
if (getValue("Nationality") != "NULL") and (getValue("Nationality") != ''):
    return "http://vocab.getty.edu/aat/300379842"
else:
    return ''
```

#### _NationalityURI_
From column: _Nationality_
``` python
if (getValue("Nationality") != "NULL") and (getValue("Nationality") != ''):
    return UM.uri_from_fields("thesauri/nationality/", getValue("Nationality"))
else:
    return ''
```


## Selections

## Semantic Types
| Column | Property | Class |
|  ----- | -------- | ----- |
| _AutryMakerURL_ | `uri` | `foaf:Document1`|
| _AutryMakerURLCopy_ | `rdfs:label` | `foaf:Document1`|
| _BirthTimespanURI_ | `uri` | `crm:E52_Time-Span1`|
| _BirthURI_ | `uri` | `crm:E63_Beginning_of_Existence1`|
| _BirthYear_ | `rdfs:label` | `crm:E52_Time-Span1`|
| _DeathTimespanURI_ | `uri` | `crm:E52_Time-Span2`|
| _DeathURI_ | `uri` | `crm:E64_End_of_Existence1`|
| _DeathYear_ | `rdfs:label` | `crm:E52_Time-Span2`|
| _EarliestBirthYear_ | `crm:P82a_begin_of_the_begin` | `crm:E52_Time-Span1`|
| _EarliestDeathDate_ | `crm:P82a_begin_of_the_begin` | `crm:E52_Time-Span2`|
| _LatestBirthYear_ | `crm:P82b_end_of_the_end` | `crm:E52_Time-Span1`|
| _LatestDeathDate_ | `crm:P82b_end_of_the_end` | `crm:E52_Time-Span2`|
| _Maker_ | `rdfs:label` | `crm:E39_Actor1`|
| _MakerAppellationURI_ | `uri` | `crm:E82_Actor_Appellation1`|
| _MakerCopy_ | `rdf:value` | `crm:E82_Actor_Appellation1`|
| _MakerURI_ | `uri` | `crm:E39_Actor1`|
| _Nationality_ | `rdfs:label` | `crm:E74_Group1`|
| _NationalityAAT_ | `uri` | `crm:E55_Type2`|
| _NationalityURI_ | `uri` | `crm:E74_Group1`|
| _ObjectURI_ | `uri` | `crm:E22_Man-Made_Object1`|
| _PreferredTermsURI_ | `uri` | `crm:E55_Type1`|
| _ProductionURI_ | `uri` | `crm:E12_Production1`|


## Links
| From | Property | To |
|  --- | -------- | ---|
| `crm:E12_Production1` | `crm:P14_carried_out_by` | `crm:E39_Actor1`|
| `crm:E22_Man-Made_Object1` | `crm:P108i_was_produced_by` | `crm:E12_Production1`|
| `crm:E39_Actor1` | `crm:P92i_was_brought_into_existence_by` | `crm:E63_Beginning_of_Existence1`|
| `crm:E39_Actor1` | `crm:P93i_was_taken_out_of_existence_by` | `crm:E64_End_of_Existence1`|
| `crm:E39_Actor1` | `crm:P107i_is_current_or_former_member_of` | `crm:E74_Group1`|
| `crm:E39_Actor1` | `crm:P131_is_identified_by` | `crm:E82_Actor_Appellation1`|
| `crm:E39_Actor1` | `foaf:homepage` | `foaf:Document1`|
| `crm:E63_Beginning_of_Existence1` | `crm:P4_has_time-span` | `crm:E52_Time-Span1`|
| `crm:E64_End_of_Existence1` | `crm:P4_has_time-span` | `crm:E52_Time-Span2`|
| `crm:E74_Group1` | `crm:P2_has_type` | `crm:E55_Type2`|
| `crm:E82_Actor_Appellation1` | `crm:P2_has_type` | `crm:E55_Type1`|
