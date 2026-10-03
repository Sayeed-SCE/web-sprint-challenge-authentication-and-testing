# Dad Jokes API: Authentication & Testing

A REST API built with Node and Express where users register, log in, and receive a **JSON Web Token**. The jokes endpoint is protected and only returns data to requests that send a valid token.

## Endpoints

| Method | Path                 | Auth  | Description                                                     |
| ------ | -------------------- | ----- | --------------------------------------------------------------- |
| POST   | `/api/auth/register` | none  | Create an account (`username`, `password`); password is hashed |
| POST   | `/api/auth/login`    | none  | Returns a welcome message and a JWT that expires in 1 day      |
| GET    | `/api/jokes`         | token | Returns the list of jokes                                       |

Send the token in the `Authorization` header.

## How it works

- Passwords are hashed with **bcrypt** before they are stored, and never saved in plain text
- Login compares the hash and signs a JWT with **jsonwebtoken**
- `restricted` middleware verifies the token and rejects missing or invalid tokens with `401`
- Validation middleware rejects missing usernames or passwords and usernames that are already taken
- Users are stored in **SQLite** through **Knex** migrations
- Integration tests use **Jest** and **Supertest** to cover registration, login and the protected route

## Running locally

```bash
npm install
npm run migrate
npm run server   # http://localhost:9000
npm test
```

Set `JWT_SECRET` in your environment for anything beyond local development.

## Tech

Node.js · Express · bcrypt · JSON Web Tokens · Knex · SQLite · Jest · Supertest · Helmet

---

Built as a sprint challenge for the [BloomTech](https://www.bloomtech.com/) Full Stack Web Development program. The original assignment brief is in [ASSIGNMENT.md](ASSIGNMENT.md).
