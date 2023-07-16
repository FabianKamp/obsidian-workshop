---
tags: paper/toread
title: "{{title}}"
{%- for creator in creators %} 
{%- if loop.first %}
{%- if creator.name == null %} 
first_{{creator.creatorType}}: {{creator.lastName}}, {{creator.firstName}} 
{%- elif creator.name %}
first_{{creator.creatorType}}: {{creator.name}}
{%- endif -%}
{%- elif loop.last %}
{%- if creator.name == null %} 
last_{{creator.creatorType}}: {{creator.lastName}}, {{creator.firstName}} 
{%- elif creator.name %}
last_{{creator.creatorType}}: {{creator.name}}
{%- endif -%}
{%- else -%}
{%- if creator.name == null %} 
{{creator.creatorType}}: {{creator.lastName}}, {{creator.firstName}}
{%- elif creator.name %}
{{creator.creatorType}}: {{creator.name}}
{%- endif -%} {%- endif -%} {%- endfor %}
year: {{date | format("YYYY")}}     
citekey: {{citekey}}
aliases: {{citekey}}
{%if itemType == "journalArticle" %}journal: {{publicationTitle}}  
{%elif itemType == "bookSection" %}book: {{publicationTitle}} 
{%- endif -%}  
volume: {{volume}} 
issue: {{issue}}    
publisher: {{publisher}}      
pages: {{pages}}   
DOI: {{DOI}}
rating: 
status: toread
---
> [! Abstract]
> {%- if abstractNote %} {{abstractNote}}  {%- endif%} {%- for attachment in attachments | filterby("path", "endswith", ".pdf") %} [pdf](file://{{attachment.path | replace(" ", "%20")}})  {%- endfor%}

> [!Cite] {{bibliography}}  

---
# synthesis
%% add > contribution:: to make it accessible in dataview%%
{% persist "synthesis" %}
{% endpersist %}

---
# figures
{% persist "figures" %}
{% endpersist %}

---
# links 
{% persist "links" %}
{% endpersist %}

---
# annotations
%% annotations imported from the pdf file %%

{% set annots = annotations %}
{%- if annots.length > 0 %}
{% for annot in annots -%} 
{%- if annot.type == "highlight" -%} 
{%- if annot.annotatedText %}  
> <mark style="background-color: {{annot.color}}">{{annot.annotatedText | nl2br}} </mark>
{%- endif -%}
{%- endif -%}  
{%- if type == "text" -%}  
Note  
{%- endif -%}  
{%- if annot.comment %}  
> **Comment**: {{annot.comment}}  
{%- endif -%}
{%- if annot.imageRelativePath %}  
![[{{annot.imageRelativePath}}]]  
{%- endif %}  
> [page {{annot.page}}](file://{{annot.attachment.path | replace(" ", "%20")}}) [[{{annot.date | format("YYYY-MM-DD")}}]]  

{% endfor -%}  
{% endif -%}

---
# references
%% list of all papers that are linked to this file %%
```dataview
TABLE first_author AS "first author", year, journal, rating 
FROM #paper AND ([[]] OR outgoing([[]]))
SORT rating asc
```
%% importDate: [[{{importDate| format("YYYY-MM-DD")}}]]  %%