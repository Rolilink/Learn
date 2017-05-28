## React Redux Modular Architecture

Structuring React-Redux into self contained and decoupled modules is important for a project to be maintainable when it scales.

### Folder Structure - Feature Oriented vs Object Role Oriented

Some frameworks like Rails follows a "Object Role Oriented" where folders are organized around the role objects play inside an application. Then objects are grouped together on this folders.

```
app/
  controllers/
  models/
  views/
```

This organizational patterns is not good for scalability since when our codebase is growing we will have to search and modify through multiple folders. A better approach will be to create a Feature Domain oriented architecture grouping files and objects in a more modular way around a Feature Domain.

```
todos/
  components/
  data/
  index.js
appointments/
  components/
  data
  index.js
```

### Rules for organizing modules

When organizing a module we have to think about some rules:
- Modules should be self-contained that enclose logic around a features domain, feature specific logic.

- Modules should be loosely coupled, this means it is not concerned or has little concern around the implementation of other modules, which directly translates to not have a hard dependency against other modules.

- Modules should expose a public API that can be accesible by others modules which could depend on this.

### Organizing React-Redux Modules

#### Data vs UI

When Organizing inside a Feature Module folder structure we can divide the module in to sections UI for React Components and Data for Redux.

```
feature-module/
  data/
  ui/
  index.js
```

#### Organizing Data with Ducks

When organizing the redux or the data part of the module, I like the approach described by erikras on ducks-modular-redux: [https://github.com/erikras/ducks-modular-redux](https://github.com/erikras/ducks-modular-redux)

#### Organizing UI

When organizing UI I like to follow a component / containers approach, this way I separate stateless from stateful components.

```
feature-module/
  ui/
    components/
    containers/
    index.js
  index.js
```

#### Organizing Constants

For constants around the module that are not redux actions, I create a `constant.js` file if this file gets too big or confusing we can break it in different files inside a `constants/` folder but having a "too big" `constant.js` file could be a signal of not separating constants domain correctly.

```
feature-module/
  index.js
  constants.js
```

#### Organizing Routes

Since each module should be self contained, it should provide it own routes to the application. I add the routes associated to a module in a `routes.js` file that exposes a configuration function that receives the route root and returns a full route

```
feature-module/
  index.js
  routes.js
```

```
// A react-router route example

import React from 'react';
import path from 'path';
import { Route } from 'react-router-dom';
import { LoginView } from './ui';


export default function authRoutes(basePath) {
  return (
    <Route path={path.join(basePath, '/login')} render={() => <LoginView />} />
  );
}
```

## Resources
- [https://medium.com/lexical-labs-engineering/redux-best-practices-64d59775802e](https://medium.com/lexical-labs-engineering/redux-best-practices-64d59775802e)
- [https://jaysoo.ca/2016/02/28/organizing-redux-application/](https://jaysoo.ca/2016/02/28/organizing-redux-application/)
- [https://marmelab.com/blog/2015/12/17/react-directory-structure.html](https://marmelab.com/blog/2015/12/17/react-directory-structure.html)