---
tag: fleeting
created:
---
# description
---
# further reading
---
# references
%% list of all papers that are linked to this file %%
```dataview
TABLE WITHOUT ID first_author AS "first author", file.link AS "File", year, journal, rating 
FROM #paper AND ([[]] OR outgoing([[]]))
SORT rating asc
```

