# Display Sorted Data with useStaticQuery in Gatsby

**[📹 Video](https://egghead.io/lessons/gatsby-display-sorted-data-with-usestaticquery-in-gatsby)**

## Showing Event Data
Our goal now is to *display event data on our page*.

In events.js:
```javascript
import {graphql, useStaticQuery } from 'gatsby';
```
And refactor EventsTemplate():
```javascript
const EventsTemplate = () => {
  const data = useStaticQuery(graphql`
      query {
        allEvent(sort: { fields: startDate, order: ASC }) {
          nodes {
            id
            name
            startDate
            endDate
            location
            url
            slug
          }
        }
      }
  `)
  const events = data.allEvent.nodes;

  return(
    <Layout>
      <EventList events={events} />
    </Layout>
  )
}
```
Above, we've defined two new components, Layout and EventList, and we've refactored the render method to use these components and pass in the events data to the EventList component.
- Layout will **define our general layout across our pages**
- EventList will **list our events**
We need to now create these two new components. Within gatsby-theme-events/src, create a components folder containing layout.js

Within layout.js, we will define our layout:
```javascript
import React from "react"

const Layout = ({ children }) => (
  <div>
    <h1>Gatsby Events Theme</h1>
    {children}
  </div>
)

export default Layout
```
Within our components folder we'll now create another file for our EventList called event-list.js.

Within that we'll define our EventList component:
```javascript
import React from "react"

const EventList = ({ events }) => (
  <pre>{JSON.stringify(events, null, 2)}</pre>
)

export default EventList
```
Now we must go back to events.js and make sure to *import these components*:
```javascript
import Layout from '../components/layout'
import EventList from '../components/event-list'
```
Now we start up our server:
```
yarn workspace gatsby-theme-events develop
```
At localhost:8000, our layout shows up containing a dump of each event and its data.

## Update the event list component to format event data
Instead of raw data, **we want to display the event data in markup**.

In event-list.js, we refactor our EventList component:
```javascript
import { Link } from 'gatsby';

const EventList = ({ events }) => (
  <>
    <h1>Upcoming Events</h1>
    <ul>
      {events.map(event => (
        <li key={event.id}>
          <strong>
            <Link to={event.slug}>{event.name}</Link>
          </strong>
          <br />
          {new Date(event.startDate).toLocaleDateString('en-US', {
            month: 'long',
            day: 'numeric',
            year: 'numeric',
          })} in {event.location}
        </li>
      ))}
    </ul>
  </>
)
```
Saving and returning to our localhost:8000 allows us to see the title and formatted date of each event, and clicking on each title allows us to see their respective page.

## Resources
- [Gatsby - Display sorted data with useStaticQuery](https://www.gatsbyjs.org/tutorial/building-a-theme/#display-sorted-data-with-usestaticquery)
