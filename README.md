# async-aws-s3-mongo-stripe-next

# 🚀 Async - open source SaaS web app. Use it as a self-hosted team communication tool or as a starting project for your own SaaS product. 🚀

https://github.com/coding-to-music/async-aws-s3-mongo-stripe-next

https://async-aws-s3-mongo-stripe-next.vercel.app

From / By https://github.com/async-labs/async

- APP: https://1.async-await.com

- API: https://api-xphxggip.async-await.com
## Environment variables:

```java
See below
```

## GitHub

```java
git init
git add .
git remote remove origin
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:coding-to-music/async-aws-s3-mongo-stripe-next.git
git push -u origin main
```


------------


## Async

Open source SaaS web app.

Async's main features are: (1) Chat for real-time, synchronous communication, (2) Discussions for asynchronous communication, (3) All communication (chats + discussions) can be organized by team.

Async was built from our popular open source [SaaS boilerplate](https://github.com/async-labs/saas). We built Async for communication within our internal team and with our clients from custom dev business. By separating synchronous (urgent) vs. asynchronous (non-urgent) conversations, we minimized distractions while working on big tasks while still reacting to urgent requests.

You can use Async as a self-hosted communication web app for your team. You can also use Async as a starting point for building a more complex SaaS web application.


## Live demo:

- APP: https://1.async-await.com
- API: https://api-xphxggip.async-await.com


## Sponsors

[![aws-activate-logo](https://user-images.githubusercontent.com/26158226/138565715-4311ddda-fb77-452a-8755-d53eb18f8645.png)](https://aws.amazon.com/activate/)

[![1password-logo](https://user-images.githubusercontent.com/26158226/138565841-ad435374-7330-477a-b6f3-2542109c3217.png)](https://1password.com/)


## Contents

- [Features](#features)
- [Run locally](#running-api-locally)
- [Deploy](#deploy-to-heroku-aws-elastic-beanstalk-api-gateway-and-aws-lambda)
- [Built with](#built-with)
- [Screenshots](#screenshots)
- [Contributing](#contributing)
- [Team](#team)


## Features

- Chat for real-time, synchronous communication
- Discussions for long-form, asynchronous communication
- Team creation, Team Member invitation, and settings for Team and User.
- Server-side rendering for fast initial load and SEO.
- User authentication with Passwordless, cookie, and session.
- Production-ready Express server with compression, parser, and helmet.
- Transactional emails (`AWS SES`): welcome, login, and team invitation.
- File upload, load, and deletion (`AWS S3`) with pre-signed request for: Comment, Message, Team Profile, and User Profile.
- Websockets with socket.io v3.
- Opinionated architecture:
  - keeping babel and webpack configurations under the hood,
  - striving to minimize number of configurations,
  - HOC extensions `MyApp` and `MyDocument`
  - server-side rendering with `Material-UI`,
  - model-specific components in addition to common components.
- Universally-available environmental variables at runtime.
- Custom logger (configure what _not_ to print in production).
- Useful components for any web app: `Confirmer`, `Notifier`, `Loading`, `MenuWithLinks`, and more.
- Production-ready, scalable architecture:
  - `app` - user-facing web app with Next/Express server, responsible for rendering pages (either client-side or server-side rendered). `app` sends requests via API methods to `api` Express server.
  - `api` - server-only code, Express server, responsible for processing requests for internal and external API infrastructures.
- **Subscriptions with `Stripe`**:
  - subscribe/unsubscribe Team to plan,
  - update card information,
  - verified Stripe webhook for failed payment for subscription.


#### Running `api` locally:

- Before running, create a `.env` file inside the `api` folder with the environmental variables as shown below.

`api/.env`:

  ```
  # Used in api/server/server.ts
  MONGO_URL_TEST=
  MONGO_URL=
  SESSION_NAME=
  SESSION_SECRET=
  
  # Used in api/server/aws-s3.ts and api/server/aws-ses.ts
  AWS_REGION=
  AWS_ACCESSKEYID=
  AWS_SECRETACCESSKEY=
  BUCKET_FOR_FILES=

  # Used in api/server/passwordless.tx and api/server/models/User.ts
  FROM_EMAIL_ADDRESS=

  ----------
  # All env variables above this line are required for successful user signup
  
  # Used in api/server/stripe.ts
  STRIPE_TEST_SECRET_KEY=
  STRIPE_LIVE_SECRET_KEY=
  STRIPE_TEST_PRICE_ID=
  STRIPE_LIVE_PRICE_ID=
  STRIPE_LIVE_ENDPOINT_SECRET=
  
  # Optionally determine the URL
  URL_APP="https://localhost:3000"
  PRODUCTION_URL_APP="https://1.async-await.com"
  API_SERVER_ENDPOINT="http://localhost:8000"
  PRODUCTION_API_SERVER_ENDPOINT="https://api-xphxggip.async-await.com"

  # Used in api/server/api/index.ts
  ENCRYPTION_KEY=

  ```
  
  - Your `.env` file file _must_ have values for the `required` variables. To use all features and third-party integrations, also add the `optional` variables.
  
  - IMPORTANT: use your values for `PRODUCTION_URL_APP` and `PRODUCTION_API_SERVER_ENDPOINT`. These are values for domain name that you own.

  - IMPORTANT: The above environmental variables are available on the server only. You should add your `.env` file to `.gitignore` inside the `api` folder so that your secret keys are not stored on a remote Github repo.

  - To get value for `MONGO_URL_TEST`, we recommend you use a [free MongoDB at MongoDB Atlas](https://docs.atlas.mongodb.com/) or [$15/month MongoDB at Digital Ocean](https://www.digitalocean.com/products/managed-databases-mongodb/)

  - Specify your own name and secret keys for Express session: [SESSION_NAME](https://github.com/expressjs/session#name) and [SESSION_SECRET](https://github.com/expressjs/session#express)

- Once `.env` is created, you can run the `api` app. Navigate to the `api` folder, run `yarn install` to add all packages, then run the command below:
  ```
  yarn dev
  ```


#### Running `app` locally:

- Navigate to the `app` folder, run `yarn` to add all packages, then run `yarn dev` and navigate to `http://localhost:3000`:

  - A `.env` file in the `app` folder is not required to run, but you can create one to override the default variables. The environmental variables for `.env` in the `app` folder are shown below.<br/>

  ```
    NEXT_PUBLIC_URL_APP="http://localhost:3000"
    NEXT_PUBLIC_PRODUCTION_URL_APP="https://1.async-await.com"

    NEXT_PUBLIC_API_SERVER_ENDPOINT="http://localhost:8000"
    NEXT_PUBLIC_PRODUCTION_API_SERVER_ENDPOINT="https://api-xphxggip.async-await.com"

    NEXT_PUBLIC_STRIPE_TEST_PUBLISHABLEKEY="pk_test_xxxxxxxxxxxxxxx"
    NEXT_PUBLIC_STRIPE_LIVE_PUBLISHABLEKEY="pk_live_xxxxxxxxxxxxxxx"
    
    NEXT_PUBLIC_API_GATEWAY_ENDPOINT=
    NEXT_PUBLIC_ENCRYPTION_KEY_FOR_EXTERNAL_SERVICES=

    NEXT_TELEMETRY_DISABLED=1
    
  ```
  
  - IMPORTANT: use your values for `NEXT_PUBLIC_PRODUCTION_URL_APP` and `NEXT_PUBLIC_PRODUCTION_API_SERVER_ENDPOINT`. These are values for domain name that you own.

  - To get `NEXT_PUBLIC_STRIPE_TEST_PUBLISHABLEKEY`, go to your Stripe dashboard, click `Developers`, then click `API keys`.

- For successful file uploading, make sure your AWS bucket has the proper CORS configuration. Go to your AWS account, find your bucket, go to `Permissions > CORS configuration`, add:

```
[
  {
    "AllowedHeaders":[
      "*"
    ],
    "AllowedMethods":[
      "PUT",
      "POST",
      "GET",
      "HEAD",
      "DELETE"
    ],
    "AllowedOrigins":[
      "http://localhost:3000",
      "https://1.async-await.com"
    ],
    "ExposeHeaders":[
      "ETag",
      "x-amz-meta-custom-header"
    ]
  }
]
```

- Make sure to update allowed origin with your actual values for `NEXT_PUBLIC_URL_APP` and `NEXT_PUBLIC_PRODUCTION_URL_APP`.

- Once `.env` is created, you can run the `app` app. Navigate to the `app` folder, run `yarn install` to add all packages, then run the command below:
  ```
  yarn dev
  ```


#### Symlink `api` in `lambda`:

In lambda directory we are symlinking api directory. You can run symlink command in lambda folder as mentioned below:
```
bash symlink ../api
```

## Deploy to Heroku, AWS Elastic Beanstalk, API Gateway and AWS Lambda

We give detailed instructions inside Chapter 9 and 10 of our SaaS Boilerplate book: https://builderbook.org/book

## Built with

- [React](https://github.com/facebook/react)
- [Material-UI](https://github.com/mui-org/material-ui)
- [Next](https://github.com/vercel/next.js)
- [MobX](https://github.com/mobxjs/mobx)
- [Express](https://github.com/expressjs/express)
- [Mongoose](https://github.com/Automattic/mongoose)
- [MongoDB](https://github.com/mongodb/mongo)
- [Typescript](https://github.com/Microsoft/TypeScript)

For more detail, check `package.json` files in both `app` and `api` folders.

To customize styles, check [this guide](https://github.com/async-labs/builderbook#add-your-own-styles).


## Screenshots

Chat for synchronous, urgent communication:<br>
<kbd>![chat-desktop](https://d2c24pn6pcl4ug.cloudfront.net/images/chat-desktop.png)</kbd>

Chat on mobile browser:<br>
<kbd><img height="700" src=https://d2c24pn6pcl4ug.cloudfront.net/images/chat-mobile.jpeg>

Discussion for asynchronous, non-urgent communication:
<kbd>![discussion](https://d2c24pn6pcl4ug.cloudfront.net/images/discussions.png)</kbd>

Discussions consist of Comments, where you can write with Markdown, preview your content, and include attachments.
<kbd>![comment](https://d2c24pn6pcl4ug.cloudfront.net/images/comment.png)</kbd>

Multiple team management demonstrated by team switcher:
<kbd>![team-switcher](https://d2c24pn6pcl4ug.cloudfront.net/images/teamswitcher2.png)</kbd>

User settings:
<kbd>![user-settings](https://d2c24pn6pcl4ug.cloudfront.net/images/account-settings.png)</kbd>

Team settings:
<kbd>![team-settings](https://d2c24pn6pcl4ug.cloudfront.net/images/team-settings.png)</kbd>

Stripe checkout:
<kbd>![stripe-checkout](https://d2c24pn6pcl4ug.cloudfront.net/images/stripe-checkout.png)</kbd>

Billing:
<kbd>![billing](https://d2c24pn6pcl4ug.cloudfront.net/images/billing.png)</kbd>


## Contributing

Want to support this project? Consider buying our [books](https://builderbook.org/).


## Team

- [Kelly Burke](https://github.com/klyburke)
- [Timur Zhiyentayev](https://github.com/tima101)

You can contact us at team@async-labs.com.

If you are interested in working with us, check out [Async Labs](https://async-labs.com/).


## License

All code in this repository is provided under the [MIT License](https://github.com/async-labs/async/blob/master/LICENSE.md).

## Project structure

```
├── api
│   ├── .elasticbeanstalk
│   │   └── config.yml
│   ├── server
│   │   ├── api
│   │   │   ├── index.ts
│   │   │   ├── public.ts
│   │   │   ├── team-leader.ts
│   │   │   └── team-member.ts
│   │   ├── models
│   │   │   ├── Chat.ts
│   │   │   ├── Comment.ts
│   │   │   ├── Discussion.ts
│   │   │   ├── EmailTemplate.ts
│   │   │   ├── Message.ts
│   │   │   └── User.ts
│   │   ├── utils
│   │   │   ├── markdownToHtml.ts
│   │   │   └── slugify.ts
│   │   ├── aws-s3.ts
│   │   ├── aws-ses.ts
│   │   ├── logs.ts
│   │   ├── passwordless-token.ts
│   │   ├── passwordless-toenstore.ts
│   │   ├── passwordless.ts
│   │   ├── robots.txt
│   │   ├── server.ts
│   │   ├── sockets.ts
│   │   └── stripe.ts
│   ├── .eslintrc.js
│   ├── .gitignore
│   ├── nodemon.json
│   ├── package.json
│   ├── tsconfig.json
│   └── yarn.lock
├── app
│   ├── .elasticbeanstalk
│   │   └── config.yml
│   ├── components
│   │   ├── chats
│   │   │   ├── ChatDetail.tsx
│   │   │   ├── ChatList.tsx
│   │   │   └── SearchWithinChat.tsx
│   │   ├── comments
│   │   │   ├── CommentContext.tsx
│   │   │   ├── CommentDetail.tsx
│   │   │   ├── CommentEditor.tsx
│   │   │   └── CommentForm.tsx
│   │   ├── common
│   │   │   ├── AvatarwithMenu.tsx
│   │   │   ├── Confirmer.tsx
│   │   │   ├── Loading.tsx
│   │   │   ├── LoginForm.tsx
│   │   │   ├── MemberChooser.tsx
│   │   │   ├── MenuWithLinks.tsx
│   │   │   ├── MenuWithMenuItems.tsx
│   │   │   ├── Notifier.tsx
│   │   │   └── SidebarListItem.tsx
│   │   ├── discussions
│   │   │   ├── DiscussionDetail.tsx
│   │   │   ├── DiscussionList.tsx
│   │   │   └── SearchDiscussions.tsx
│   │   ├── layout
│   │   │   ├── index.tsx
│   │   │   └── menu.ts
│   │   ├── messages
│   │   │   ├── MessageContent.tsx
│   │   │   ├── MessageDetail.tsx
│   │   │   ├── MessageEditor.tsx
│   │   │   └── MessageForm.tsx
│   │   ├── settings
│   │   │   └── SettingsMenu.tsx
│   │   ├── teams
│   │   │   ├── CreateTeamModal.tsx
│   │   │   └── InviteMemberModal.tsx
│   ├── lib
│   │   ├── api
│   │   │   ├── makeQueryString.ts
│   │   │   ├── sendRequestAndGetResponse.ts
│   │   │   ├── to-api-server-public.ts
│   │   │   ├── to-api-server-team-leader.ts
│   │   │   ├── to-api-server-team-member.ts
│   │   │   └── to-external-services.ts
│   │   ├── store
│   │   │   ├── Chatts
│   │   │   ├── Comment.ts
│   │   │   ├── Discussion.ts
│   │   │   ├── Message.ts
│   │   │   ├── Team.ts
│   │   │   ├── User.ts
│   │   │   └── index.ts
│   │   ├── confirm.ts
│   │   ├── highlightSearchResult.ts
│   │   ├── isMobile.ts
│   │   ├── notify.ts
│   │   ├── resizeImage.ts
│   │   ├── sharedStyles.ts
│   │   └── theme.ts
│   ├── pages
│   │   ├── public
│   │   │   ├── login.tsx
│   │   │   └── register.tsx
│   │   ├── settings
│   │   │   ├── my-account.tsx
│   │   │   ├── my-billing.tsx
│   │   │   └── team-settings.tsx
│   │   ├── _app.tsx
│   │   ├── _document.tsx
│   │   ├── chat.tsx
│   │   └── discussion.tsx
│   ├── public/fonts
│   │   ├── IBM-Plex-Mono
│   │   │   ├── IBMPlexMono-Regular.woff
│   │   │   └── IBMPlexMono-Regular.woff2
│   │   ├── Roboto
│   │   │   ├── Roboto-Regular.woff
│   │   │   └── Roboto-Regular.woff2
│   │   ├── cdn.css
│   │   └── server.css
│   ├── server
│   │   └── server.ts
│   ├── .babelrc
│   ├── .eslintignore
│   ├── .eslintrc.js
│   ├── .gitignore
│   ├── next-env.d.ts
│   ├── next.config.js
│   ├── nodemon.json
│   ├── package.json
│   ├── tsconfig.json
│   ├── tsconfig.server.json
│   └── yarn.lock
├── lambda
│   ├── src
│   │   └── checkCardExpiration.ts
│   ├── .eslintrc.js
│   ├── .gitignore
│   ├── api
│   ├── handler.ts
│   ├── package.json
│   ├── serverless.yml
│   ├── tsconfig.json
│   ├── tslint.json
│   └── yarn.lock
├── .gitignore
├── LICENSE.md
├── README.md
```
