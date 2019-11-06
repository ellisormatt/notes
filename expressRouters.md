# Express Routers

- an express router provides a subset of Express methods
- to use: *mount* the router at a certain path using app.use() and pass in the router as the second argument
    - the router will now be used for all paths tht begin with that path segment
    ```js
    const express = require('express');
    const app = express();

    const monsters = {
        '1': {
            name: 'godzilla',
            age: 250000000
        },
        '2': {
            Name: 'manticore',
            age: 21
        }
    }

    const monstersRouter = express.Router();

    app.use('/monsters', monstersRouter);

    monstersRouter.get('/:id', (req, res, next) => {
        const monster = monsters[req.params.id];
        If (monster) {
            res.send(monster);
        } else {
            res.status(404).send();
        }
    });
    ```

- best practice is to keep each router in its own file


