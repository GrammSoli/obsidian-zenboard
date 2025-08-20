<%*
const title = tp.file.title || tp.date.now("GGGG-[W]WW");
const weekStart = moment(title, "GGGG-[W]WW").startOf("isoWeek");
const weekEnd = weekStart.clone().endOf("isoWeek");
const year = weekStart.format("YYYY");
const week = weekStart.format("WW");
const prev = weekStart.clone().subtract(1,"week").format("GGGG-[W]WW");
const next = weekStart.clone().add(1,"week").format("GGGG-[W]WW");
const monthLink = weekStart.format("YYYY-MM");
_%>
---
год: <%= year %>
неделя: <%= week %>
период_с: <%= weekStart.format("YYYY-MM-DD") %>
период_по: <%= weekEnd.format("YYYY-MM-DD") %>
---
# Неделя <%= title %>

[[<%= prev %>]] | [[<%= next %>]]
Месяц: [[<%= monthLink %>]]

## Итоги

