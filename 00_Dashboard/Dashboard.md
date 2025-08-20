# <% tp.date.now("HH:mm") %> — <% tp.date.now("dddd, DD MMMM YYYY") %>

## Quick Links
- [[<%= tp.date.now("YYYY-MM-DD") %>|Сегодня]]
- [[<%= tp.date.now("GGGG-[W]WW") %>|Текущая неделя]]
- [[<%= tp.date.now("YYYY-MM") %>|Текущий месяц]]
- [[<%= tp.date.now("YYYY") %>|Год]]
- [[06_GeneralUseful/Notes/Inbox|Входящие]]
- Последние ресурсы
```dataview
LIST FROM "" WHERE тип="ресурс" SORT создано desc LIMIT 5
```

## Overview
```dataviewjs
const pages = dv.pages("");
const topics = pages.where(p => p.тип == "тема");
const topicsClosed = topics.where(p => p.выполнено);
const tasks = pages.file.tasks;
const totalTasks = tasks.length;
const doneTasks = tasks.filter(t=>t.completed).length;
dv.table(["Метрика","Значение"], [
  ["Всего тем", topics.length],
  ["Тем закрыто", topicsClosed.length],
  ["Всего задач", totalTasks],
  ["Закрыто задач", doneTasks]
]);
```

### Ресурсы за месяц
```dataview
TABLE length(rows) AS "Количество"
GROUP BY формат
FROM ""
WHERE тип="ресурс" AND dateformat(создано, "yyyy-MM") = dateformat(date(now), "yyyy-MM")
```

<div class="card-grid">
<div class="card">
#### Темы прогресса
```dataviewjs
const topics = dv.pages('').where(p => p.тип == 'тема');
const groups = topics.groupBy(p => p.сфера);
const rows = groups.map(g => {
  const tasks = g.rows.flatMap(r => r.file.tasks);
  const total = tasks.length;
  const done = tasks.filter(t=>t.completed).length;
  return [g.key, total, done, total ? Math.round(done/total*100) : 0];
});
dv.table(['Категория','Задачи','Выполнено','%'], rows);
```
</div>
<div class="card">
#### Активные проекты
```dataviewjs
const projects = dv.pages('').where(p => p.тип == 'проект' && p.статус != 'завершен');
const rows = projects.map(p => {
  const tasks = p.file.tasks;
  const total = tasks.length;
  const done = tasks.filter(t=>t.completed).length;
  const prog = total ? Math.round(done/total*100) : 0;
  return [p.file.link, p.статус, p.дедлайн, prog + '%'];
});
dv.table(['Проект','Статус','Дедлайн','Прогресс'], rows);
```
</div>
<div class="card">
#### Ресурсы в работе
```dataview
TABLE статус, создано
FROM ""
WHERE тип="ресурс" AND contains(['reading','listening','watching'], статус)
SORT создано desc
LIMIT 10
```
</div>
<div class="card">
#### Цели на сегодня
```dataview
TASK
FROM "01_Journaling/Day"
WHERE file.name = dateformat(date(now), "yyyy-MM-dd")
```
</div>
</div>

## ADHD
```dataview
LIST FROM "02_ADHD/Tools","02_ADHD/Research"
SORT file.ctime desc
LIMIT 5
```

## Read&Listen
```dataview
LIST FROM "03_Read&Listen"
SORT file.ctime desc
LIMIT 5
```

## Teaching
```dataview
LIST FROM "04_Teaching"
SORT file.ctime desc
LIMIT 5
```

## Entertainment
```dataview
LIST FROM "05_Entertainment"
SORT file.ctime desc
LIMIT 5
```

## Business
```dataview
LIST FROM "07_Business"
SORT file.ctime desc
LIMIT 5
```

## Languages
```dataview
LIST FROM "08_Languages"
SORT file.ctime desc
LIMIT 5
```

## On this day
```dataview
LIST FROM "01_Journaling/Day"
WHERE dateformat(дата, "MM-DD") = dateformat(date(now), "MM-DD") AND dateformat(дата, "YYYY") < dateformat(date(now), "YYYY")
SORT дата
```

