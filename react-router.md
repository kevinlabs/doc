React Router Cheatsheet

basic usage
```js
import { default as Router, Route } from 'react-router'

const routes = (
  <Route>
    <Route path='*' handler={RootView} />
  </Route>
)

Router.run(routes, Router.HashLocation, (Root) => {
  React.render(<Root />, document.getElementById('all'))
})
```

nested routes
```js
const routes = (
  <Route handler={Chrome}>
    <Route path='about' handler={About} />
    <Route path='inbox' handler={Inbox} />
    <Route path='messages/:id' handler={Message} />
  </Route>
)

import { RouteHandler } from 'react-router'

const Chrome = React.createClass({
  render () {
    return (
      <div>
        <h1>App</h1>
        <RouteHandler />
      </div>
    )
  }
})
```

url params
```js
var Message = React.createClass({
  componentDidMount: function () {
    // from the path `/inbox/messages/:id`
    var id = this.props.params.id
    ...
```

link
```js
import { Link } from 'react-router'

<!-- make a named route `user` -->
<Link to='user' params={{userId: 10}} />

<Link to='login'
  activeClassName='-active'
  onClick='...'>

```

other configs
```js
<Route path='/'>
  <DefaultRoute handler={Home} />
  <NotFoundRoute handler={NotFound} />

  <Redirect from='login' to='sessions/new' />
  <Redirect from='login' to='sessions/new' params={{from: 'home'}} />
  <Redirect from='profile/:id' to='about-user' />

  <Route name='about-user' ... />
```

router.create
```js
var router = Router.create({
  routes: <Route>...</Route>,
  location: Router.HistoryLocation
})

router.run((Root) => { ... })
```

navigation
```js
import { Navigation } from 'react-router'

React.createClass({
  mixins: [ Navigation ], ...
})

this
  .transitionTo('user', {id: 10})
  .transitionTo('/path')
  .transitionTo('http://...')
  .replaceWith('about')
  .makePath('about') // return URL
  .makeHref('about') // return URL
  .goBack()
```
