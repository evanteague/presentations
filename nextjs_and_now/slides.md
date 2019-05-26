### So you want to make an app but don't want to deal with setting up infrastructure

*Disclaimer*: I'm not an expert

---

## Next JS
![](./images/whynextjs.png)

---

## Routing

- Requires a "pages" directory
    - One of only 2 folders that Next requires you to have

- Provides a `<Link />` Higher Order Component (HOC)
    - Navigates on the client

---

## Routing (continued)
```
import Link from 'next/link'

const Index = () => (
  <div>
    <Link href="/about">
      <a>About Page</a>
    </Link>
    <p>Hello Next.js</p>
  </div>
)

export default Index
```

---

## Routing - Route Masking
- Show a different url in browser than what you’re linking to in the code
    - e.g. `www.myUrl/postId=12345?feature` becomes ` www.myUrl/TitleOfPost`
- By default, only works through client side routing and not on the server
- However, you can get these cleaner URLs using server side routing (e.g. Express)

---

## Hydrating your app with initial data

- Built in `getInitialProps` function
- Calls on the server
- When using the `<Link />` component to navigate, it does so on the client and thus make API calls on the client, but if you go to the page directly it does it on the server.

---

## `getInitialProps` Example
```
GameDisplay.getInitialProps = async function() {
    const response = await axios.get(apiUrl, {
        params: {
            day: 1,
            month: '03',
            year: 2018, 
            seasonPart: 'regular',
        }
    });

    return {
        stats: response.data,
    };
}
```

---

## styled-jsx
- Next comes with styled-jsx built in

- styled-jsx is a library, similar to styled-components
    - Rules are scoped to the component
    - There’s a way to do global styles (for those curious)

---

## Why styled-jsx?
- Problematic trying to render CSS with SSR because Node doesn’t understand CSS
    - Have to use something like web pack to compile it
    - Basically, if you try to require in a CSS file on the server, Node will be like “I don’t understand that” and bomb out

- Hence, we use something like styled-jsx because it's just a template string and babel can parse it

---

## Other details
- Works with npm packages and components
    - ...depending on how the creator exported their package
- Uses normal React (hooks, imports/exports, etc), nothing special
- Support for CSS preprocessors (with some configuration, but it's really easy)
- [More](https://nextjs.org/docs)

---

## Setting up NextJs
- Your normal Node project setup stuff...`npm init`, etc
- 
```
npm i next
```
- In `package.json`
```
"scripts": {
    "dev": "NODE_ENV=development next dev",
    "build": "next build",
    "start": "NODE_ENV=production next start",
    "now-build": "next build"
  }
```
- Run `npm run dev`

---

# THAT'S IT!

---

## Now
![](./images/whynow.png)

---

## What's so great about Now?
- The easiest deployment system I've ever seen
- Rebuilds only what changed in your app
- Serverless (uses Lambdas)
    - Low cost
    - Automatically scales based on usage

---

## Why serverless is good
> One of the main benefits is that the developer only needs to reason about one concurrent computation happening in the context of their code, despite many of them being able to run in parallel.

---

## Why serverless is good (continued)
> In contrast, processes and containers tend to expose an entire server as their entrypoint. That server would then define code for handling many types of requests.

---

## Now - Scalability
- Scalabality
    - Servers: we developers have to manage when to scale our apps based on metrics (CPU, memory). This takes alot of our time because these metrics can shift so much that we have to constantly adjust it.
    - Lambdas: 1 request --> new Lambda invocation

---

## Now - Code splitting
- Now does a sort of "code-splitting" where it only loads the part of the function that is necessary (e.g. They hit the `/get` endpoint, it just loads the code for that path)

---

## Now - Builders
- Now has built in support which allows these features

<img src="./images/now_builders.png" width="300px" height="400px">

---

## What if I need to create a backend API?
- You can do it!

## Setting up Now (for a NextJs project)
- Create an account at [Now](https://zeit.co/now)

- Install Now
```
npm i -g now
```
- Then run
```
now login
```
It will send you an email verifying your identity

---

## Setting up Now (continued)
- Add `"now-build": "next build"` to your `package.json` file
- Create a now.json file
```
{
    "version": 2,
    "name": "app name",
    "builds": [{ "src": "package.json", "use": "@now/next" }]
}
```

---

## Setting up Now (continued)
- If you haven't done so already, create a `next.config.js` file with
```
module.exports = {
    target: 'serverless',
};
```

6. Type `now`

---

# THAT'S IT!

---

## A couple of gotchas
- Make sure you're up to date with both NextJs and Now
- Remember: If you want to use ES6 features on the server, you need something to transpile it
    - NextJS has this built in
    - Express does not
- Typescript support with Now seems iffy
    - Maybe it's just me

## Sources
- https://nextjs.org/learn/basics/getting-started
- https://nextjs.org/docs
- https://zeit.co/now
- https://zeit.co/docs/v2/deployments/concepts/lambdas/

---

## Demo

