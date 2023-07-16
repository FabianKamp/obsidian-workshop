---
tags: [permanent/todo] 
aliases:
---
# description
---
# papers
---
# references
%% list of all the paper linked to this note %%
```dataview
TABLE first_author AS "first author", year, journal, rating 
FROM #paper AND ([[]] OR outgoing([[]]))
SORT rating asc
```
