---
layout: post
title: "LFE Friday - calendar:day_of_the_week/3"
description: ""
category: tutorials
tags: [lfe friday,lfe,erlang]
author: Robert Virding
---
{% include JB/setup %}
{% include LFEFriday/setup %}

Today’s LFE Friday covers [calendar:day_of_the_week/3](http://www.erlang.org/doc/man/calendar.html#day_of_the_week-3).

``calendar:day_of_the_week/3`` allows you to get the day of the week a day occurred on when passed a year, a month and a day.

The first argument represents the year and must be a non-negative integer. The second argument is the month and must be an integer value between 1 and 12 inclusive, representing the 12 months of the Gregorian Calendar, with January being month one. The final argument to ``calendar:day_of_the_week/3`` is the date, and is expected to be a integer between 1 and 31 inclusive.

``calendar:day_of_the_week/3`` returns an integer value in between 1 and 7 inclusive, with a return value of 1 representing Monday, and a 7 being Sunday.

```lisp
> (calendar:day_of_the_week 1 1 1)
1
> (calendar:day_of_the_week 1970 1 1)
4
> (calendar:day_of_the_week 1999 12 31)
5
> (calendar:day_of_the_week 0 1 1)     
6
```

As you can see that the publish date of this LFE Friday post[^1], 2015-04-10, returns a 5, which is in fact a Friday according to Erlang.

```lisp
> (calendar:day_of_the_week 2015 4 10)
5
```

There is also a ``calendar:day_of_the_week/1`` function which has all the same constraints but instead of taking three arguments, takes one argument that is a three-tuple of the year, month, and day.

```lisp
> (calendar:day_of_the_week #(2015 4 10))
5
> (calendar:day_of_the_week #(1970 1 1)) 
4
> (calendar:day_of_the_week #(1999 12 31))
5
```

And in the spirit of helping to recognize error messages when we see them, let’s take a look at what we get when we pass some invalid inputs to ``calendar:day_of_the_week/3``.

```lisp
> (calendar:day_of_the_week 0 0 0)        
exception error: function_clause
  in (: calendar date_to_gregorian_days 0 0 0)
  in calendar:day_of_the_week/3 (calendar.erl, line 151)
> (calendar:day_of_the_week 1970 2 31)   
exception error: if_clause
  in calendar:date_to_gregorian_days/3 (calendar.erl, line 116)
  in calendar:day_of_the_week/3 (calendar.erl, line 151)
> (calendar:day_of_the_week 1970 13 2)
exception error: function_clause
  in (: calendar last_day_of_the_month1 1970 13)
  in calendar:date_to_gregorian_days/3 (calendar.erl, line 115)
  in calendar:day_of_the_week/3 (calendar.erl, line 151)
```

If you look at the error messages you see that ``calendar:day_of_the_week/3`` calls ``calendar:date_to_gregorian_days/3``, which we will cover in next week’s LFE Friday.

–Proctor, Robert

[^1]: At least the day which should be the publish day.
