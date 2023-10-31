# using-t3

The T3 stack is unbelievably powerful. But, because it's a bit new, you can't just Google anything you want and find 20 samples. So here are some notes I've created that hopefully can answer a lot of basic questions.

## Creating a New Project

This is following mostly Theo's suggestions in the [intro video](https://create.t3.gg/en/introduction) that I saw in October 2023. But some things weren't available then, such as app router for Next.

I may have enhanced a few steps or modified them.

1. Go to [create t3 page](create.t3.gg) and click the copy button, then run where you want the directory for your new app to appear.
2. choose `pnpm` (used below) or whatever option you prefer.
3. I suggest `app router` which is not the default.
4. add it to your workspace in VS or open it.
5. move into it's directory in a VS terminal
6. commit to git `git add -a && git commit -m "init"
7. Go to GitHub and create the repo
8. copy from the code to push from an existing repo on the command line
9. run dev locally: `pnpm run dev`

## Deploy on Vercel

1. you need to set your secret key: run `openssl rand -base64 32` in the terminal
2. open your `.env` file and insert something like this:

   ```env
    NEXTAUTH_SECRET="<generated-secret-key>"
    NEXTAUTH_URL="http://localhost:3000"
   ```

3. go to vercel.com and set up a new project. You have to have vercel linked to your GitHub and choose your project
4. go to configuration and you just have to copy your `.env` and paste it into the variable field to copy over secrets. Then you just hit save.
5. make sure it's deploying.

## Add a Real Database

1. go to [PlanetScale](https://planetscale.com/) and set up a db there. Unfortunately, you will need to put in a CC to use them. You are allowed one free project per card.
2. create a prisma database url, and then paste into your `.env` file replacing `DATABASE_URL`. Remove the old `DATABASE_URL` from Vercel and paste in the new.

## Add Auth

1. go to Clerk and set up.



   Axiom
   Upstash
   Turborepo

Static: Astro

restart TS server: command-P “Typescript: Restart TS server”
With Prisma
Save changes (required to do every time): `npx prisma db push`
Make the data types available for your code: `npm i`
See your or add to it: (close and reset your app after any changes to the prisma schema, then…) `npx prisma studio`

# How To on Server

get a Prisma type: `import type { <TypeName> } from “@prisma/client”`
get the db on the server `import { db} from ‘~/server/db’`
call a procedure: DON’T. extract an async func that does the essential same thing and reuse

# How To on Client

import the api: `import { api } from ‘~/utils/api’`
call a tRPC procedure: `api.<router>.<function>.useQuery();` (or `useMutation()` as the case may be)

GitHub
set up ci: Theo used Ask ChatGPT: `Write me a minimal github ci .yml workflow file that installs node modules, runs typescript typechecking, and also runs lint. This repo uses npm`. I found that it was a disaster. Used outdated versions of certain actions that led to a lot of problems. So if you do that, go to the actions on GitHub and update whatever ChatGPT provides with the latest. You also may need to add some secrets if it complains. I had to add 4. But make sure to put “fake” or something for their values.

Next
speed up build s: in `next.config.mjs` add to `config`:

typescript: {
ignoreBuildErrors: true,
},
eslint: {
ignoreDuringBuilds: true,
},
swcMinify: true,
