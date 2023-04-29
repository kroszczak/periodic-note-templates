<%* let calendarDate = '{{title}}' -%>
<%*
pDate = calendarDate.split('-')
currentDate = new Date(pDate[2], pDate[1]-1, pDate[0]);
startDate = new Date(currentDate.getFullYear(), 0, 1);
days = Math.floor((currentDate - startDate)/(24 * 60 * 60 * 1000));
weekNumber = Math.ceil(days / 7);
year = currentDate.getFullYear()
output = `${year}-W${('0' + weekNumber).slice(-2)}`
%>
> [!METADATA]-

> - Created:: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
> - Updated:: <% tp.date.now("YYYY-MM-DD @ HH:mm") %>
> - ID:: <% tp.date.now('YYYYMMDDHHmm') %>
> - week:: <% output %>
> - calendarDate:: <% '{{title}}' %>


**Table of Contents:**
```toc
style: number
```

___

## Memos
- …

^memo-link

## Work Log
- …

^work-link

## Trackers
### Statistics
- Feeling:: 
- Learnt Word:: 
- Money Spent:: 
- Panic:: 
- Prayer:: 
- Steps:: 
- Hours Worked:: 

### Habits
- Anki:: 
- Coffee:: 
- Exercise:: 
- Martial Arts:: 
- Reading:: 
- Revision:: 
- Shower::
- Typing:: 

### Weather
- Temperature:: 
- Feels Like:: 
- Weather:: 
- Wind Direction:: 
- Wind Speed:: 
- Observed:: 

## Tasks
### Not Done
```tasks
not done
hide backlink
path includes 02.01 Periodic Notes

heading does not include Day Planner
heading does not include Before Heading Out…
```

### New Today
- [ ]