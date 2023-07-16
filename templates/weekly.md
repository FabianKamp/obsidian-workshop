---
tag: journal/weekly
date: {{date:YYYY-[W]WW}}
aliases:
---
# agenda
```mermaid 
gantt 
	dateFormat YY-MM-DD 
	axisFormat %Y-%m-%d
	title Calendar

	section example project 
	first part: p1, 2023-07-01, 14d
	second part: v2, 2023-07-11, 1M
```
--- 
# weekly summary session
---
# open tasks 
```dataview 
TASK FROM #journal/daily   
WHERE !completed
SORT due asc, text asc
GROUP BY tag
```
---
# daily journal
```dataview 
TABLE file.cday AS "created" 
FROM #journal/daily AND ([[]] OR outgoing([[]]))
SORT file.name desc 
```
