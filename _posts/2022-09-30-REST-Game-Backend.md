---
title: "Creating a useful REST game backend"
date: 2022-09-30
---

## Why?
Sometimes we want our game's client (e.g. Unity) to share information with other players. A classic example of this is a high-score system where each player can see the top score in the world in a high score display.

**The components**
- NodeJS REST server (to handle requests from the client)
- Postgres Database to persist the game's data
- A docker file to define the components

**NodeJS REST server**
components
- Express (to set up all needed REST requests)
- Jest (to set up tests for the project)
- Husky (use git commit hooks to run tests)

**Integrated testing**
One option to guarantee (at least in terms of regression) the quality of a software project is through automated testing. For a server one solution could be to use a git hook (e.g. using Husky) in combination with a testing framework like Jest. By combining these two tools it is possible to make sure that no code is committed which breaks any of the test. One classic test example for a server might be a classic test request.

Knock'em is a 3D arcade bowling game for mobile phones in which players use a bowling to knock over pins to earn points. An example `get` request to get all players might look like this:

```js
const getPlayers = (request, response) => {
    pool.query('SELECT * FROM players', (error, results) => {
        if (error) {
            throw error
        }
        response.status(200).json(results.rows)
    })
}
```

## Limitations
The backend will not support WebRTC/similar persistent connections out of the box.

## Deploying
The code for the server and database will need a place to live. After trying different methods (e.g. port forwarding an old laptop, heroku, etc.) a rented server is used because it allows for the most flexibility at a cheap price (3€/month). The package of the server is a docker-compose file. The entire project is pulled in regular intervals (e.g. daily) and the server is restarted.