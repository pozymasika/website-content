---
title: How to check if a date refers to a day in the past in JavaScript
description: "Given a JavaScript date, how do you check if it references a day in the past?"
date: 2019-10-16T07:00:00+02:00
tags: js
---

I had this problem: I wanted to check if a date referred to a past day, compared to another date.

Just comparing them using `getTime()` was not enough, as dates could have a different time.

I ended up using this function:

```js
const firstDateIsPastDayComparedToSecond = (firstDate, secondDate) => {
  if (firstDate.setHours(0,0,0,0) - secondDate.setHours(0,0,0,0) >= 0) { //first date is in future, or it is today
    return false
  }

  return true
}
```

I use `setHours()` to make sure we compare 2 dates at the same time (00:00:00).