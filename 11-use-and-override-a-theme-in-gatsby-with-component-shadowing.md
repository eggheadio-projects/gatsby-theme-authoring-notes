# Use and Override a Theme in Gatsby with Component Shadowing

**[📹 Video](https://egghead.io/lessons/gatsby-use-and-override-a-theme-in-gatsby-with-component-shadowing)**

To use the theme we defined in the previous lesson, we need to use *component shadowing* in order to override the default theme in gatsby-plugin-theme-ui
- *“Component shadowing” is a mechanism to override the default rendering provided by a Gatsby theme*
- Check out [resources](#resources) for a blog post on component shadowing.

In gatsby-theme-events/src, we create a folder **with the same name as the theme in the source field**, and we *"shadow"* the index.js where the theme is defined.

In other words, in gatsby-theme-events/src, create gatsby-theme-ui/index.js

Within gatsby-theme-ui/index.js:
```javascript
import { theme } from "../theme"

export default theme
```
Now we'll refactor our **Layout** component to use Theme UI.

Within layout.js:
```javascript
import React from "react"
import { Layout as ThemeLayout, Header, Main, Container } from 'theme-ui';

const Layout = ({ children }) => (
  <ThemeLayout>
  <Header><h1>Gatsby Events Theme</h1></Header>
    <Main>
      <Container>{children}</Container>
    </Main>
  </ThemeLayout>
)

export default Layout
```
We can now check if this works:
```
yarn workspace site develop
```
## Resources
- [Gatsby - Use and override a theme with component shadowing](https://www.gatsbyjs.org/tutorial/building-a-theme/#use-and-override-a-theme-with-component-shadowing)
-[Gatsby - What is Component Shadowing?](https://www.gatsbyjs.org/blog/2019-04-29-component-shadowing/)
