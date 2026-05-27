---
name: Vercel Deploy Helper
description: Use this skill when the user asks to deploy the application to Vercel.
---

# Instructions

When deploying this Vue application to Vercel:
1.  Ensure all dependencies are installed (`npm install`).
2.  Run the build command to ensure there are no compilation errors (`npm run build`).
3.  If Vercel CLI is not installed, prompt the user to let you install it (`npm i -g vercel`).
4.  Run the `vercel` command to initiate the deployment.
5.  Run `vercel --prod` if the user specifies a production deployment.
6.  Print out the final deployment URL for the user.
