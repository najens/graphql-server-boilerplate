# GraphQL Server Boilerplate

A boilerplate GraphQL server with:

- [GraphQL Yoga](https://github.com/prisma/graphql-yoga) for a Scalable GraphQL server (based on based on Apollo Server & Express)
- [Prisma](https://www.prisma.io/) for a GraphQL database ORM (running on MySQL)
- [GraphQL Playground](https://github.com/prisma/graphql-playground)
- [Nodemon](https://github.com/remy/nodemon) to automatically restart the server when code changes are made
- [Dotenv](https://github.com/motdotla/dotenv) to handle environment variables
- JWT Authentication built in
- Example models for Users and Posts

*Originally based on [node-graphql-server](https://github.com/graphql-boilerplates/node-graphql-server)*

## Requirements

- Node, NPM and Yarn
- Prisma CLI installed globally - `yarn global add prisma`

## Getting started

```sh
# 1. Install dependencies
yarn

# 2. Prisma DB
# - Sign up to prisma.io, add a new service (follow the prompts)
# - Copy `.env.example` to `.env` and add your endpoint/keys
# - Deploy to Prisma
yarn deploy-db

# 3. Start server (runs playground on http://localhost:4000)
yarn start
```

## Deploying to Production

```sh
# 1. Deploy the database (eg. to Prisma)
yarn deploy-db

# 2. Setup the environment variables on the server, as seen in `.env`
```

---

## User / Authentication

### Sign Up

```
mutation {
  signup(
    email: "zeus@examples.com"
    password: "secret42"
    name: "Zeus"
  ) {
    token
    user {
      id
      name
      email
    }
  }
}
```

### Login

```
mutation {
  login(
    email: "zeus@examples.com"
    password: "secret42"
  ) {
    token
    user {
      email
    }
  }
}
```

### Me
*Requires `"Authorization": "Bearer ...""` header*

```
query {
  me {
    id
    name
    email
    posts {
      title
      published
    }
  }
}
```

---

## Posts

### Create Draft Post
*Requires `"Authorization": "Bearer ...""` header*

```
mutation {
  createDraft(
    title: "New Draft Post"
    content: "Hello new post that's not posted yet"
  ) {
    id
    title
    content
    author {
      name
    }
  }
}
```

### Publish one of my Draft Posts
*Requires `"Authorization": "Bearer ...""` header*

```
mutation {
  publish(id: "cjt6q05lh2qi70b45gkux1gfv") {
    id
    title
    content
    published
    author {
      name
    }
  }
}
```

### Delete one of my Posts
*Requires `"Authorization": "Bearer ...""` header*

```
mutation {
  deletePost(id: "cjt6q6des2shk0b45gtusvd9d") {
    id
    title
  }
}
```

### Feed of All Published Posts

```
query {
  feed {
    id
    title
    content
    author {
      name
    }
  }
}
```

### Feed of My Drafted Posts
*Requires `"Authorization": "Bearer ...""` header*

```
query {
  drafts {
    id
    title
    content
    author {
      name
    }
  }
}
```