# Create Data Driven Pages in Gatsby with GraphQL and createPages

**[📹 Video](https://egghead.io/lessons/gatsby-create-data-driven-pages-in-gatsby-with-graphql-and-createpages)**

## Create pages for event previews and individual event pages

To begin our last step in gatsby-node.js, we set up the call to create the root page:
```javascript
exports.createPages = async ({ actions, graphql, reporter }) => {
  const basePath = '/';
  actions.createPage({
    path: basePath,
    component: require.resolve('.src/templates/events.js')
  });
```
The basePath defaults to the root path, and the createPage method creates a page at the basePath.

Next, we'll set it up so we can query for events.

The following will allow us to retrieve all events, sorted by start date, in ascending order, and will allow us to handle the error in case the GraphQL query failed.
```javascript
  const result = await graphql(`
    query {
      allEvent(sort: { fields: startDate, order: ASC }) {
        nodes {
          id
          slug
        }
      }
    }
  `);

  if(result.errors) {
    reporter.panic('error loading events', reporter.errors);
    return;
  }
```
Next, we'll create a page for each event by grabbing the event nodes queried from GraphQL, looping through the events, and using createPage.
```javascript
  const events = result.data.allEvent.nodes;

  events.forEach(event => {
    const slug = event.slug;

    actions.createPage({
      path: slug,
      component: require.resolve('./src/templates/event.js'),
      context: {
        eventID: event.id
      }
    });
  });
}
```
Now, we need to actually create the event.js and events.js components.

First, create src/templates/events.js within gatsby-theme-events. Within events.js:
```javascript
import React from 'react';

const EventsTemplate = () => <p>TODO build the events page</p>;

export default EventsTemplate;
```
Then, create an event.js within src/templates, and within that:
```javascript
import React from 'react';

const EventTemplate = () => <p>TODO build the events page</p>;

export default EventTemplate;
```
We can now run Gatsby in development mode:
```
yarn workspace gatsby-theme-events develop
```
And navigate to localhost:8000 to see "TODO build the events page"

We can also navigate to localhost:8000/404 to see the pages for each of our events.

## Resources
- [Create data-driven pages using GraphQL and createPages](https://www.gatsbyjs.org/tutorial/building-a-theme/#create-data-driven-pages-using-graphql-and-createpages)
