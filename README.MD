## Setup

```
Run: nvm use
Run: yarn
Run: yarn generate-types
Run: yarn dev
```

## Fixed bugs

- Use production GraphQL instead of staging
- apollo nuxt.config.js httpEndpoint or statement
- Moved files to right folder following atomic design system
- Introduced new components
- Added NavBar component inside DefaultTemplate
- Introduced NuxtLink instead of @click with $emit
- Moved data fetching to page level
- Introduced detail page based on title (for SEO / readability) with ID as queryparameter because ID is required to retrieve a post. Cannot use title only to retrieve a post and page also needs to keep working if you navigate directly to it via url.
- Added error message for PostsList and PostView
- Added checks for data using v-if
- Use scss global variables instead of fixed values
- Concept for skeleton loading
- Introduced new GraphQL query for post
- Page title and page detail title using head()

## Missing improvements

- Use and extend title global styles (%text-style-title1) for titles and subtitles on pages
- Refactor names of colors
- Make constants dynamic instead of static constants via env variables
