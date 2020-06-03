# Consume a Theme in a Gatsby Application

**[📹 Video](https://egghead.io/lessons/gatsby-consume-a-theme-in-a-gatsby-application)**

## Set up a new Gatsby site
Open up your terminal, move into a new folder, and create a new directory called theme-test:
```
mkdir theme-test
```
Change directories to this new directory:
```
cd theme-test/
```
Set up the project:
```
yarn init -y
```
Now add your packages, including the theme you just made:
```
yarn add react react-dom gatsby @yournpmusername/gatsby-theme-events
```
**Note:** If you didn't publish a theme, use @jlengstorf/gatsby-theme-events instead.
Open up your theme-test folder and make a gatsby-config.js.

Inside, create a module.exports, and add your theme in the plugins array:
```javascript
module.exports = {
  plugins: ["@jlengstorf/gatsby-theme-events"],
}
```

## Install the Gatsby CLI
Run the following in termianl:
```
yarn global add gatsby-cli
```
## Run the site
To start the site, run the following in the terminal at the /theme-test directory:
```
gatsby develop
```
At localhost:8000, we can see our theme installed.

To add some data, create a data/events.yml in the root project folder.

In the events.yml:
```
- name: Party
  location: My House
  start_date: 2019-06-26
  end_date: 2019-06-26
  url: https://jason.af/party
```
Back at localhost:8000 we can see our event displayed with just a few lines of code.
## Resources
- [Lesson 13 Code](https://github.com/ParkerGits/authoring-gatsby-themes/tree/13-consume-a-theme-in-a-gatsby-application)
- [Consume a theme in a Gatsby application](https://www.gatsbyjs.org/tutorial/building-a-theme/#consume-a-theme-in-a-gatsby-application)
