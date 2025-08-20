<%*
const title = tp.file.title || tp.date.now("YYYY");
_%>
---
год: <%= title %>
---
# Год <%= title %>

```dataview
LIST from "01_Journaling/Month"
WHERE год = <%= title %>
SORT file.name asc
```

