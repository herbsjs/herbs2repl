# herbs2repl
Herbs REPL

![Herbs REPL](./doc/render1607020056527.gif)

### Installing
```
    $ npm install @herbsjs/herbs2repl
```

### Using

`src/domain/usecases/_uclist.js`:
```javascript
module.exports = (injection) => {
    return [
        { usecase: require('./createItem').createItem(injection), tags: { group: 'Items' } },
        { usecase: require('./updateItem').updateItem(injection), tags: { group: 'Items' } },
        ...
     ]
}
```

`src/infra/repl/index.js`:
```javascript
const usecases = require('../../domain/usecases/_uclist')
const repl = require('@herbsjs/herbs2repl')

const main = async (injection) => {

    // list of all use cases, initialized
    const ucs = usecases(injection)

    // your user for the REPL session
    const user = {
        canAddItem: true, canCreateList: true, canDeteleList: false,
        canGetLists: true, canUpdateItem: true, canUpdateList: true
    }

    repl(ucs, user, {groupBy: "group"})
}

main().then()
```

Then run on your terminal:

     $ node ./src/infra/repl
