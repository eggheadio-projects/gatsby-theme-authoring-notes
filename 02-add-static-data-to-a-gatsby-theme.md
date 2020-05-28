# Add Static Data to a Gatsby Theme

**[📹 Video](https://egghead.io/lessons/gatsby-add-static-data-to-a-gatsby-theme)**

## events.yml

In our gatsby-theme-events folder, add a new folder named "data" and within that create an events.yml file.

In the events.yml file, paste in the following:
```
- name: React Rally
  location: Salt Lake City, UT
  start_date: 2019-08-22
  end_date: 2019-08-23
  url: https://www.reactrally.com/

- name: DinosaurJS
  location: Denver, CO
  start_date: 2019-06-20
  end_date: 2019-06-21
  url: https://dinosaurjs.org/

- name: JSHeroes
  location: Cluj-Napoca, Romania
  start_date: 2020-04-23
  end_date: 2020-04-24
  url: https://jsheroes.io/

- name: The Lead Developer
  location: Austin, TX
  start_date: 2019-11-08
  end_date: 2019-11-08
  url: https://austin2019.theleaddeveloper.com/
```

In order to read the .yaml file above, we must install new dependencies as follows:
```
yarn workspace gatsby-theme-events add gatsby-source-filesystem gatsby-transformer-yaml
```

Next, within the gatsby-theme-events folder, create a gatsby-config.js

Following the lesson, our gatsby-config.js should look like:
```javascript
module.exports = {
  plugins: [
    {
      resolve: 'gatsby-source-filesystem',
      options: {
        path: 'data'
      }
    },
    {
      resolve: 'gatsby-transformer-yaml',
      options: {
        typeName: 'Event'
      }
    }
  ]
}
```
After running
```
yarn workspace gatsby-theme-events develop
```
We can access GraphQL at localhost:8000/\_\_\_graphql

Opening up allEvent then nodes on the side bar allows us to query properties of our events.


## Resources
- [Gatsby Plugin Configuration](https://www.gatsbyjs.org/docs/gatsby-config/#plugins)
- [YAML Syntax](https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html)
