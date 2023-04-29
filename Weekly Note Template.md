---
tags:
- "#calendar/weekly/<% tp.date.now('YYYY') %>"
banner: "![[<% tp.date.now('YYYY MMMM') %> Weekly Banner.jpg]]"
banner_icon: 🗓️
---
<%*
title = '{{title}}'
title = title.split('-')
y = title[0]
w = parseInt(title[1].slice(1))
simple = new Date(y, 0, 1 + (w - 1) * 7);
dow = simple.getDay();
ISOweekStart = simple;
if (dow <= 4)
    ISOweekStart.setDate(simple.getDate() - simple.getDay() + 1);
else
    ISOweekStart.setDate(simple.getDate() + 8 - simple.getDay());
WeekStart = `${('0'+ISOweekStart.getDate()).slice(-2)}-${('0'+(ISOweekStart.getMonth()+1)).slice(-2)}-${ISOweekStart.getFullYear()}`
%>

# {{title}}

# Work Log
- [[EverydayNotes/Days/<% tp.date.weekday("DD-MM-YYYY", 0, WeekStart, "DD-MM-YYYY") %>|Monday]]
	![[EverydayNotes/Days/<% tp.date.weekday("DD-MM-YYYY", 0, WeekStart, "DD-MM-YYYY") %>#^work-link]]
- [[EverydayNotes/Days/<% tp.date.weekday("DD-MM-YYYY", 1, WeekStart, "DD-MM-YYYY") %>|Tuesday]]
	![[EverydayNotes/Days/<% tp.date.weekday("DD-MM-YYYY", 1, WeekStart, "DD-MM-YYYY") %>#^work-link]]
- [[EverydayNotes/Days/<% tp.date.weekday("DD-MM-YYYY", 2, WeekStart, "DD-MM-YYYY") %>|Wednesday]]
	![[EverydayNotes/Days/<% tp.date.weekday("DD-MM-YYYY", 2, WeekStart, "DD-MM-YYYY") %>#^work-link]]
- [[EverydayNotes/Days/<% tp.date.weekday("DD-MM-YYYY", 3, WeekStart, "DD-MM-YYYY") %>|Thursday]]
	![[EverydayNotes/Days/<% tp.date.weekday("DD-MM-YYYY", 3, WeekStart, "DD-MM-YYYY") %>#^work-link]]
- [[EverydayNotes/Days/<% tp.date.weekday("DD-MM-YYYY", 4, WeekStart, "DD-MM-YYYY") %>|Friday]]
	![[EverydayNotes/Days/<% tp.date.weekday("DD-MM-YYYY", 4, WeekStart, "DD-MM-YYYY") %>#^work-link]]
- [[EverydayNotes/Days/<% tp.date.weekday("DD-MM-YYYY", 5, WeekStart, "DD-MM-YYYY") %>|Saturday]]
	![[EverydayNotes/Days/<% tp.date.weekday("DD-MM-YYYY", 5, WeekStart, "DD-MM-YYYY") %>#^work-link]]
- [[EverydayNotes/Days/<% tp.date.weekday("DD-MM-YYYY", 6, WeekStart, "DD-MM-YYYY") %>|Sunday]]
	![[EverydayNotes/Days/<% tp.date.weekday("DD-MM-YYYY", 6, WeekStart, "DD-MM-YYYY") %>#^work-link]]

## Overview
### Week Statistics
```dataviewjs
const daysPath = dv.current().file.folder;

const attributes = {
	'panic': {
		label: 'Panic',
		average: 10,
	},
	'money-spent': {
		label: 'Money Spent',
		backgroundColor: 'rgba(85, 174, 229, 0.2)',
		borderColor: 'rgba(85, 174, 229, 1)',
		average: 20,
	},
	'prayer': {
		label: 'Prayer',
		backgroundColor: 'rgba(255, 211, 101, 0.2)',
		borderColor: 'rgba(255, 211, 101, 1)',
		average: 5,
	},
	'steps': {
		label: 'Steps',
		backgroundColor: 'rgba(141, 82, 188, 0.2)',
		borderColor: 'rgba(141, 82, 188, 1)',
		average: 10000,
	},
	'hours-worked': {
		label : 'Hours Worked',
		backgroundColor: 'rgba(143, 208, 50, 0.2)',
		borderColor: 'rgba(143, 208, 50, 1)',
		average: 6
	},
};
const ws = "<% WeekStart %>"
const date = "<% tp.date.now('DD-MM-YYYY') %>";

customJS.DvCharts.renderWeeklyChart({
	dv,
	context: this,
	daysPath: 'EverydayNotes/Days',
	attributes,
	type: 'average',
	date,
	ws
})
```

```dataview
TABLE WITHOUT ID
	link(file.name) as "Day",
	feeling AS "💭",
	money-spent AS "💸",
	panic AS "🌪️",
	prayer AS "🕋",
	steps AS "👣",
	kod AS "✏️"
FROM "EverydayNotes/Days"
WHERE icontains(week, this.file.name)
SORT file.name ASC
```

### Habits
```dataview
TABLE WITHOUT ID
	file.link AS "Day",
	anki AS "📇",
	coffee AS "☕",
	exercise AS "🏋️",
	martial-arts AS "🥋",
	reading AS "👓",
	revision AS "🔁",
	shower AS "🚿",
	typing AS "⌨️"
FROM "EverydayNotes/Days"
WHERE icontains(week, this.file.name)
SORT file.name ASC
```

### Learnt Words
```dataviewjs
dv.table(
	["Learnt Word", "Meaning"],
	dv.pages('"EverydayNotes/Days"')
	.filter(p => p["Learnt Word"] && p.week.path == "<% tp.date.now("YYYY [Week] WW") %>")
	.sort(p => dv.date(p.file.name), 'asc')
	.flatMap(p =>
		Array.from(
			{
				length: Math.floor(
					p["Learnt Word"].length / 2
				)
			},
			(_, i) => [
				`${'**'}${p["Learnt Word"][i * 2]}${'**'}`,
				p["Learnt Word"][(i * 2) +1]
			]
		)
	)
)
```

### Weather
```dataview
TABLE WITHOUT ID
	file.link AS Day,
	weather AS ☁️,
	(temperature + " °C") AS 🌡️,
	(feels-like + " °C") AS 💭,
	wind-direction AS 🧭,
	(wind-speed + " km h⁻¹") AS 🍃,
	observed AS 🕓
FROM "EverydayNotes/Days"
WHERE icontains(week, this.file.name)
SORT file.name ASC
```


> [!METADATA]-
> Created:: [[<% tp.date.now('DD-MM-YYYY') %>]] <% tp.date.now('HH:mm') %>
> Updated:: <% tp.date.now('DD-MM-YYYY HH:mm') %>
> ID:: <% tp.date.now('YYYYMMDDHHmmss') %>
> TitleWeek:: <% '{{title}}' %>
> WeekStart:: <% WeekStart %>