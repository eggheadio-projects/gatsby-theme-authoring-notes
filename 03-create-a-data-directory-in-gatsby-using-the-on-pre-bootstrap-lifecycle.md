# Create a Data Directory in Gatsby using the onPreBootstrap lifecycle

**[📹 Video](https://egghead.io/lessons/gatsby-create-a-data-directory-in-gatsby-using-the-onprebootstrap-lifecycle)**

## gatsby-node.js
Within the gatsby-theme-events folder, create a file named gatsby-node.js

In our gatsby-node.js, we need to
1. Make sure the data directory exists
2. Define the event type
3. Define resolvers for any custom fields (slug)
4. Query for events and create pages

## Making sure the data directory exists
If you fire up your theme, and the “data” directory doesn’t exist, gatsby-source-filesystem will throw an error. To guard against this, you’ll use the onPreBootstrap API hook to check if the data directory exists, and, if not, create it:


Within gatsby-node.js:
```javascript
const fs = require('fs');

exports.onPreBootstrap = ({ reporter }) => {
  const contentPath = 'data';

  if (!fs.existsSync(contentPath)) {
    reporter.info(`creating the ${contentPath} directory`);
    fs.mkdirSync(contentPath);
  }
};
```
With this code, if the data directory doesn't exist, it will create it. Now we have ensured that the data directory exists.


## Resources
- [Gatsby - Create a data directory using the onPreBootstrap lifecycle](https://www.gatsbyjs.org/tutorial/building-a-theme/#create-a-data-directory-using-the-onprebootstrap-lifecycle)
