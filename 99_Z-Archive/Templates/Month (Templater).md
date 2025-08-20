<%*
const title = tp.file.title || tp.date.now("YYYY-MM");
const monthStart = moment(title, "YYYY-MM");
const year = monthStart.format("YYYY");
const month = monthStart.format("M");
_%>
---
месяц: <%= title %>
год: <%= year %>
---
# Месяц <%= title %>

```dataview
LIST from "01_Journaling/Week"
WHERE год = <%= year %> AND date(период_с).month = <%= month %>
SORT file.name asc
```

