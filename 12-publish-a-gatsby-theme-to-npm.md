# Publish a Gatsby Theme to npm

**[📹 Video](https://egghead.io/lessons/gatsby-publish-a-gatsby-theme-to-npm)**

## Publishing our Theme
In this lesson we'll learn how to make your Gatsby theme available for use by anyone in the community.

We first need to update our package.json before publishing our theme to npm.

In gatsby-theme-events/package.json, we want to namespace our theme in order to keep track of who published the theme and to avoid naming collisions:
```javascript
{
  "name": "@jlengstorf/gatsby-theme-events",
  "version": "1.0.0",
  // ...
}
```
We need to now make sure we're logged in to npm.

In the terminal:
```
npm whoami
```
If you haven't already authorized your user for your machine, it will ask you to run
```
npm adduser
```
The terminal will now prompt you for a username, password, and email.

For the sake of following along with the lesson, the namespace in your package.json will need to be your own.

Change directories into the gatsby-theme-events directory:
```
cd gatsby-theme-events/
```
and publish:
```
npm publish --access public
```

You can now access npm and view your published package.
## Resources
- [Gatsby - Publish a theme to npm](https://www.gatsbyjs.org/tutorial/building-a-theme/#publish-a-theme-to-npm)
