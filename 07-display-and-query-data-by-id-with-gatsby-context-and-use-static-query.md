# Display and Query Data by id with Gatsby context and useStaticQuery

**[📹 Video](https://egghead.io/lessons/gatsby-display-and-query-data-by-id-with-gatsby-context-and-usestaticquery)**

## Individual Event Pages
Our goal now is to **create a template React component for each individual Event page**.

In event.js:
```javascript
import { graphql } from 'gatsby'

export const query = graphql`
  query($eventID: String!) {
    event(id: { eq: $eventID }) {
      name
      url
      startDate(formatString: "MMMM D, YYYY")
      endDate(formatString: "MMMM D, YYYY")
      location
      slug
    }
  }
`;
```
Now in our **EventTemplate** component, we *pass in anything that goes into a page query as a data prop*, and we *refactor the component to use the Layout component*
```javascript
const EventTemplate = ({ data: { event } }) => (
  <Layout>
    <Event {...event} />
  </Layout>
)
```
We've defined a new **Event** component above which will take in each event data node as a prop.

We must now create this **Event** component. In our components folder, create an event.js, and within:
```javascript
import React from 'react';

const Event = props => <pre>{JSON.stringify(props, null, 2)}</pre>

export default Event;
```
Moving back to templates/event.js, we import our new **Event** component and our **Layout** component to use:
```javascript
import Layout from '../components/layout';
import Event from '../components/event';
```
Back at our localhost:8000, we can click on one of our events to view the data associated with that event.

## Update the event component to format event data
Again, our page displays raw data, so **our goal now is to display the data as markup**. In components/event.js, we refactor our **Event** component:
```javascript
const Event = ({ name, location, url, startDate, endDate }) => (
  <div>
    <h1>{name} ({location})</h1>
    <p>
      {startDate}-{endDate}
    </p>
    <p>
      Website: <a href={url}>{url}</a>
    </p>
  </div>
)
```
Our event data for individual event pages is now formatted.
## Resources
- [Gatsby - Display and query data by id with context and static queries](https://www.gatsbyjs.org/tutorial/building-a-theme/#display-and-query-data-by-id-with-context-and-static-queries)
