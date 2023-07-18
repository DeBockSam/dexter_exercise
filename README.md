# DEXTER EXERCISE

This exercise is created to get you familiar with the basic principles of next.js (13).\
What you start with here is whatever you get after running the following command: `npx create-next-app@latest`
with options eslint / typescript / tailwindcss enabled.

## Step 1: List page (Home) (make a list of all pokémon)

- Transform the homepage into a list of pokémon fetched from the pokémon api.

Tips:

- https://pokeapi.co/docs/v2#resource-listspagination-section
- https://pokeapi.co/docs/v2#pokemon-section
- Some components / api calls can already be found in ... to speed up this process.

## Step 2: Detail page (per pokémon)

- Every pokémon in the list can be clicked to show a detail view of the pokémon (other page)
- Both should be able to fetch everything Server side so all should be server components a.t.m.
- (title with name / image (so we can test next/image))

## Step 3: Static vs. dynamic routes

- Place a console.log() in the Home page & the Detail page's render fn.
- During development you will see every re-render logged, as everything is dynamically rendered during development.
- Build the site & start it (npm run build, npm run start)
- You will notice that the home page is static & the detail page is dynamic. (circles / lamda)
- Home page log should already have happened during build.
- Detail page will render every time you navigate to one.
- Notice the links prefetching detail pages on the home page.

## Step 4: static parameters

- Our server now needs to render a pokémon detail page every time a pokémon is visited. We want to lower the load by statically rendering the most visited pokémon [1,2,3,25]

Tips:

- generateStaticParams

## Step 5: Route handlers

As next.js runs on nodejs, you can also create route handlers.

- Create a route handler with which we can fetch the same list of pokémon.
- Will fetching to this from our homepage work? Why yes or no?

## STEP 6: Static / dynamic or Incremental static generation (ISG)

- lets add a string representing the date/time we fetched to our fetch result.
- A.t.m. we have a static generated page build @ build time. (If the application is build it should stay the same date until build again)
- Add the no-store or revalidate: 0 to our fetch options. (build the site & look how it behaves)
- Now add the revalidate option to your fetch. (build again, you should see the date change only after your revalidate time)

Info:
You could force these values for the whole page.tsx with route-segment-config options
(https://nextjs.org/docs/app/api-reference/file-conventions/route-segment-config)

(EXTRA QUESTION): In the last question of step 3 we statically pre-rendered a few detail pages of pokémon. Could we make it so only those pokémon routes are available & others return a 404?
(Tip for extra question: use the info of this step :) )

## Step 7: Server components vs. client components

Until now we could solve all with server components.
Everything could be fully pre-rendered on the server. So a.t.m. our react just receives HTML & doesn't need to do any hydration etc. All our fetch logic etc. is also not send to the client side, keeping our bundle size to a minimum.
What if we want to add some functionality that would be needed on the client side.

- We can handle the filtering server or client side.
- add a loading.tsx to show when we are fetching the list. (this is actually a suspense boundary, you can toggle this via react developer tools. Or place timeout in our api call so you can see it more clearly if you want)
- add error.tsx (force an error. You should see the error message)
- Filter / search in list: name / number / type

Tips:

- Try to separate the components that need "use client" from the ui that doesn't need it as much as possible. This will result in more RSC (react server side components)

## STEP 8 (EXTRA) Layout + Advanced routing

- When on homepage i want the detail to open up in a modal / or to the side when i click on it instead of linking through to the detail route. While still being able to refresh the page, share the page use backwards navigation to go to the list & reopen the modal again on forwards navigation.

Tips:
- Intercepting Routes + Parallel routes
