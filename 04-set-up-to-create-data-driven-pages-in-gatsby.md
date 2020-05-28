# Set up to Create Data Driven Pages in Gatsby

**[📹 Video](https://egghead.io/lessons/gatsby-set-up-to-create-data-driven-pages-in-gatsby)**

## Defining the event type
To satisfy condition 2 in our list, we add the following to gatsby-node.js
```javascript
exports.sourceNodes = ({ actions }) => {
  actions.createTypes(`
    type Event implements Node @dontInfer {
      id: ID!
      name: String!
      location: String!
      startDate: Date! @dateformat @proxy(from: "start_date")
      endDate: Date! @dateformat @proxy(from: "end_date")
      url: String!
      slug: String!
    }
  `)
}
```

Note: for startDate and endDate, because the camel case does not line up with start_date and end_date, we include the following on the ends of each respectively:
```
@proxy(from: "start_date")
```
```
@proxy(from: "end_date")
```

We now need to define a custom resolver for our slug field, as we don't have a slug field in our events.

## Defining resolvers for custom fields (slug)
To gatsby-node.js, add the following:
```javascript
exports.createResolvers = ({ createResolvers }) => {
  const basePath = '/'

  const slugify = str => {
    const slug = str
      .toLowerCase()
      .replace(/[^a-z0-9]+/g, '-')
      .replace(/(^-|-$)+/g, '');
    return `/${basePath}/${slug}`.replace(/\/\/+/g, '/');
  }

  createResolvers({
    Event: {
      slug: {
        resolve: source => slugify(source.name)
      }
    }
  })
}
```

The resolver above returns the "slugified" version of the event name.

Documentation on Javascript Regular Expressions can be found in the [resources](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions). Otherwise, the instructor does a good job of explaining what the function does, so if you aren't familiar with Regular Expressions, just take the instructor's word for it.

## GraphQL
Running the following allows us to open our project in development mode:
```
yarn workspace gatsby-theme-events develop
```
Open up localhost:8000/\_\_\_graphql to view our newly formatted event nodes

The event type Date allows us to view relative time or formatted time for our startDate and endDate

## Resources
- [Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)
- [Gatsby - Define the Event type](https://www.gatsbyjs.org/tutorial/building-a-theme/#define-the-event-type)
- [Gatsby - Define resolvers for any custom fields (slug)](https://www.gatsbyjs.org/tutorial/building-a-theme/#define-resolvers-for-any-custom-fields-slug)
