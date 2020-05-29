# Style and Format Dates in React

**[📹 Video](https://egghead.io/lessons/gatsby-style-and-format-dates-in-react)**

## Display reader-friendly dates
We're now going to take a look at **styling and formatting dates in React**.

At the moment, *we are currently displaying the date by separating the startDate and the endDate with a hyphen*, **but this isn't ideal**.

We're going to *refactor the Event component to improve the way that the date is displayed*.
- If the event is one day, we want it to display like June 21 2019
- For events spanning multiple days, we want the date to look like June 21-23 2019
- If the event spans across months, we want it to look like June 30-July 2 2019
In components/event.js, we create an EventDate component:
```javascript
const getDate = (date, { day = true, month = true, year = true } = {}) =>
  date.toLocaleDateString("en-US", {
    day: day ? "numeric" : undefined,
    month: month ? "long" : undefined,
    year: year ? "numeric" : undefined,
  })
const EventDate = ({ startDate, endDate }) => {
  const start = new Date(startDate)
  const end = new Date(endDate)
  const isOneDay = start.toDateString() === end.toDateString()
  return (
    <>
      <time dateTime={start.toISOString()}>
        {getDate(start, { year: isOneDay })}
      </time>
      {!isOneDay && (
        <>
          –
          <time dateTime={end.toISOString()}>
            {getDate(end, { month: start.getMonth() !== end.getMonth() })}
          </time>
        </>
      )}
    </>
  )
}
```
We can now refactor our **Event** component to include **EventDate**:
```javascript
const Event = ({ name, location, url, startDate, endDate }) => (
  <div>
    <h1>{name} ({location})</h1>
    <p>
      <EventDate startDate={startDate} endDate={endDate} />
    </p>
    <p>
      Website: <a href={url}>{url}</a>
    </p>
  </div>
)
```
We can now view our pages on localhost:8000 and see that our one day, multiple day, and multiple month event dates are being displayed correctly.

## Personal Issues
For me personally, the dates for multiple day events were not displaying as they did in the video. For example, on the DinosaurJS page, the date was displayed as

June 20-2019 (day:21)

instead of

June 20-21 2019

This may be due to a change in toLocaleDateString() or due to my own personal settings. If you also encounter this issue and have an easy fix, please feel free to contribute!
## Resources
- [Lesson 8 Code](https://github.com/ParkerGits/authoring-gatsby-themes/tree/08-style-and-format-dates-in-react)
- [Gatsby - Style and format dates in React](https://www.gatsbyjs.org/tutorial/building-a-theme/#style-and-format-dates-in-react)
- [JavaScript Date Object Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
