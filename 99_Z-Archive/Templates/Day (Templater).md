<%*
const title = tp.file.title || tp.date.now("YYYY-MM-DD");
const weekLink = moment(title, "YYYY-MM-DD").format("GGGG-[W]WW");
const weekNum = moment(title, "YYYY-MM-DD").format("WW");
const year = moment(title, "YYYY-MM-DD").format("YYYY");
_%>
---
дата: <%= title %>
год: <%= year %>
неделя: <%= weekNum %>
---
# День <%= title %>

[[<%= weekLink %>]]

## Задачи

- [ ] 

## Итоги

