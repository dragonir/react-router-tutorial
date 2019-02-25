<img src="https://s3.amazonaws.com/devmountain/readme-logo.png" width="250" align="right">

# 项目概述

在这个项目中，我们将为一所大学构建一个网站，用于追踪学生信息和班级注册信息。在不同视图（views）之间，我们将使用React Router进行导航，花些时间来熟悉我们已经提供给你的以下组件。

* `App` 将会作为我们应用的最顶层组件。
* `Home` 将作为应用首次加载时的主页，它也将展示大学的班级信息.
* `About` 将作为展示大学相关信息的页面。
  * `History` 将作为about页面的镶嵌视图，用于展示大学的历史信息。
  * `Contact` 将作为about页面的镶嵌视图，用于展示大学的联系信息。
* `ClassList` 用于展示所有注册学生的具体课程。
* `Student` 用于展示受欢迎学生的详细信息。

# 在线预览

<a href="https://devmountain.github.io/react-4-afternoon/#/">点击我查看示例</a>

<img src="https://github.com/DevMountain/react-4-afternoon/blob/solution/readme-assets/1.png" />

## 安装

* `fork` 和 `clone` 这个仓库。
* 使用 `cd` 命令进入项目目录 。
* 运行 `npm install`。
    *  `json-server` 是安装的依赖中的其中一个包。
    * 这个库将模拟一个 REST api，使得你可以使用 HTTP 请求获取学生数据。
      * 这些数据被储存在 `./db.json`。
    * 另一个为你安装的库是 `concurrently`。
    * 这个库允许我们在单个终端窗口中运行多个脚本。
* 运行 `npm start` 来开启开发服务器 <b>以及</b> `json-server`.

<img src="https://github.com/DevMountain/react-4-afternoon/blob/solution/readme-assets/2.png" />

## 步骤 1

### 概括

在这一步，我们将安装配置react router所需要的额外配置，然后我们将创建一个该项目所需要的路由。

### 操作指引

* 安装 React Router (`npm install --save react-router-dom`)。
* 在`./src`目录下创建一个名为 `routes.js`的文件，并打开它。
* 在该文件中进行路由配置: 
  * 将以下组件作为routes:
    * `./src/components/Home/Home.js`
    * `./src/components/About/About.js`
  * 在你的路由中使用以下路径和组件组合:
    * Path: "/" - Component: `Home` - 这个路径应该是 exact.
    * Path: "/about" - Component: `About`.

<details>

<summary> 详细说明 </summary>

<br />

Let's begin by installing the `react-router-dom` package. This will allow us to use routing in a react application. We can install it by running `npm install --save react-router-dom` in a terminal. Make sure the terminal is `cd` into the root project directory.

Now that we have `react-router-dom`, let's create a JavaScript file that will hold all of our routes. In `.src/`, let's make a new file called `routes.js`. At the top of this file we'll need to import `React` from `react` and also import `Switch` and `Route` from `react-router-dom`.

```js
import React from 'react';
import { Switch, Route } from 'react-router-dom';
```

We'll also want to import the components that we want the user to be able to route to. In this case, let's import the `Home` and `About` component.

```js
import React from 'react';
import { Switch, Route } from 'react-router-dom';
import Home from './components/Home/Home';
import About from './components/About/About';
```

Now that we have all of our dependencies in `routes.js`, we can use an `export default` statement to export a router. We'll need an `exact` route at `/` to load the `Home` component and a route at `/about` to load the `About` component.

```js
export default (
  <Switch>
    <Route component={ Home } exact path="/" />
    <Route component={ About } path="/about" />
  </Switch>
)
```

</details>

### 答案

<details>

<summary> <code> ./src/routes.js </code> </summary>

```js
import React from 'react';
import { Switch, Route } from 'react-router-dom';
import Home from './components/Home/Home';
import About from './components/About/About';

export default (
  <Switch>
    <Route component={ Home } exact path="/" />
    <Route component={ About } path="/about" />
  </Switch>
)
```

</details>

## 步骤 2

### 概括

在这一步中，我们将把在`./src/routes.js`中配置的路由添加到我们的应用 `./src/index.js` 中。

### 操作指引

* 打开 `./src/index.js`.
* Import `HashRouter` from `react-router-dom`.
* Wrap the `App` component in a `HashRouter` component.
* Open `./src/App.js`.
* Import `routes` from `./routes.js`.
* Underneath the `nav` element render the `routes` JSX.

<details>

<summary> 详细说明 </summary>

<br />

Let's begin by opening `./src/index.js` and importing `HashRouter` from `react-router-dom` at the top of the component. We'll need to wrap our react application with this `HashRouter` component in order for routing to work.

```js
ReactDOM.render(
  <HashRouter>
    <App />
  </HashRouter>
, document.getElementById('root'));
```

Now that our application is wrapped with `HashRouter`, we can render our router any where in the app. Let's open `./src/App.js` and import `./src/routes.js` at the top of the file. Then, in the `render` method, let's render our routes underneath the `nav` element.

```js
render() {
  return (
    <div>
      <nav className='nav'>
        <div>WestSide University</div> 
        <div className='link-wrap'>
          <div className='links'>Home</div>
          <div className='links'>About</div> 
        </div>
      </nav>

      { routes }
    </div>
  )
}
```

</details>

### 答案

<details>

<summary> <code> ./src/index.js </code> </summary>

```js
import React from 'react';
import ReactDOM from 'react-dom';
import { HashRouter } from 'react-router-dom';
import './main.css';
import App from './App';

ReactDOM.render(
  <HashRouter>
    <App />
  </HashRouter>
, document.getElementById('root'));
```

</details>

<details>

<summary> <code> ./src/App.js </code> </summary>

```js
import React, { Component } from 'react';
import routes from './routes';

export default class App extends Component {
  render() {
    return (
      <div>
        <nav className='nav'>
          <div>WestSide University</div> 
          <div className='link-wrap'>
            <div className='links'>Home</div>
            <div className='links'>About</div> 
          </div>
        </nav>

        { routes }
      </div>
    )
  }
}
```

</details>

<img src="https://github.com/DevMountain/react-4-afternoon/blob/solution/readme-assets/3.png" />

## 步骤 3

### 概括

在这一步中，我们将添加链接，来渲染我们的home和about视图。

### 操作指引

* 打开 `src/App.js`.
* 从 `react-router-dom` 引入 `Link` .
* 找到className为 `links`的 `div` 元素：
  * 将 `div` 元素替换为 `Link` 组件.
  * Home 的链接应该被设置为 `/`.
  * About 的链接应该被设置为 `/about`.

<details>

<summary> 详细说明 </summary>

<br />

Let's begin by opening `src/App.js` and importing `Link` from `react-router-dom` at the top of the file. The `Link` component will allow us to add clickable links into the DOM so the user can navigate the application. There are two `div` elements with the classname of `links`. Let's replace the `div` to be `Link` with the same classname. The `Link` component uses a `to` prop to determine which route to navigate to. For the home route, we'll want to use `/`, and for the about route, we'll want to use `/about`.

```js
<Link to="/" className='links'>Home</Link>
<Link to="/about" className='links'>About</Link> 
```

</details>

### 答案

<details>

<summary> <code> ./src/App.js </code> </summary>

```js
import React, { Component } from 'react';
import { Link } from 'react-router-dom';
import routes from './routes';

export default class App extends Component {
  render() {
    return (
      <div>
        <nav className='nav'>
          <div>WestSide University</div> 
          <div className='link-wrap'>
            <Link to="/" className='links'>Home</Link>
            <Link to="/about" className='links'>About</Link>
          </div>
        </nav>

        { routes }
      </div>
    )
  }
}
```

</details>

<br />

<img src="https://github.com/DevMountain/react-4-afternoon/blob/solution/readme-assets/4g.gif" />

## 步骤 4

### 概括

在这一步中，我们将为 `ClassList` 组件添加一个新的路由，我们将同样在 `Home` 组件中添加 `Link` 组件，为每个列出的课程（数学、英语、生物）添加路由。`ClassList` 组件将需要为学生渲染一个具体课程，为了实现该功能，我们需要使用route params路由参数。

### 操作指引

* 打开 `src/routes.js`。
* 引入`ClassList` 组件，将其作为一个路由。
* 创建一个 `ClassList` 路由，携带以下特性：
  * Path: `/classlist/:class` - Component: `ClassList`.
* 打开 `src/Home/Home.js`.
* 引入 `Link` from `react-router-dom`。
* 对每个 `button` 元素使用一个 `Link` 组件包裹.
* 每个链接应该跳转到 `/classlist` ，并且携带以下参数：
  * Math 1010 - `/classlist/MATH1010`
  * English 2010 - `/classlist/ENG2010`
  * Biology 2020 - `/classlist/BIO2020`

<details>

<summary> 详细说明 </summary>

<br />

Let's begin by opening `src/routes.js` and importing the `ClassList` at the top of the file with the other imported components. For this component, we are going to make use of routing parameters. This will allow us to use a single component that can know what dataset to load by looking at the parameter. For example: the math parameter will be `MATH1010`, when the component loads and reads `MATH1010` we can select all the students from `db.json` with the class of `MATH1010`. If that doesn't make sense entirely don't worry, we'll go into more detail in later steps.

For now let's add a new route that uses a path of `/classlist/:class` and uses a component of `ClassList`. The `:class` indicates a route parameter called `class` in the url. We'll cover how to access the route parameter in a later step.

```js
<Route component={ ClassList } path="/classlist/:class" />
```

Now that we have our new route setup in `./src/routes.js`, let's open up `./src/components/Home/Home.js` and import `Link` from `react-router-dom` at the top of the file. The `Home` component renders three buttons for the classes, let's update those buttons to be wrapped in a `Link` component. For Math, we'll want to route `/classlist/MATH1010`. For English, we'll want to route to `/classlist/ENG2010`. And for Biology, we'll want to route to `/classlist/BIO2020`. If you're wondering why it's specifically `MATH1010`, `ENG2010`, and `BIO2020`; it's so that we can map over the `db.json` and make a `class` match. A student's `class` property will equal one of those three strings.

```js
render() {
  return (
    <div className="box">
      <Link to='/classlist/MATH1010'><button className='btn'>Math 1010</button></Link>
      <Link to='/classlist/ENG2010'><button className='btn'>English 2010</button></Link>
      <Link to='/classlist/BIO2020'><button className='btn'>Biology 2020</button></Link>
    </div>
  );
}
```

</details>

### 答案

<details>

<summary> <code> ./src/routes.js </code> </summary>

```js
import React from 'react';
import { Switch, Route } from 'react-router-dom';
import Home from './components/Home/Home';
import About from './components/About/About';
import ClassList from './components/ClassList/ClassList';

export default (
  <Switch>
    <Route component={ Home } exact path="/" />
    <Route component={ About } path="/about" />
    <Route component={ ClassList } path="/classlist/:class" />
  </Switch>
)
```

</details>

<details>

<summary> <code> ./src/components/Home/Home.js </code> </summary>

```js
import React, { Component } from 'react';
import { Link } from 'react-router-dom';

export default class Home extends Component {

  render() {
    return (
      <div className="box">
        <Link to='/classlist/MATH1010'><button className='btn'>Math 1010</button></Link>
        <Link to='/classlist/ENG2010'><button className='btn'>English 2010</button></Link>
        <Link to='/classlist/BIO2020'><button className='btn'>Biology 2020</button></Link>
      </div>
    );
  }
}
```

</details>

<br />

<b>当页面间导航变化时观察URL的变化</b>

<img src="https://github.com/DevMountain/react-4-afternoon/blob/solution/readme-assets/5g.gif" />

## 步骤 5

### 概括

在这一步中，我们将更新 `ClassList` 组件中学生注册的具体课程。为了拿到这些数据，我们将通过向我们的 `json-server` 进行 `HTTP` 请求，查询 `class` 路由参数等于什么。

### 操作指引

* 打开 `src/components/ClassList/ClassList.js`。
* 创建一个构造函数，初始化一个带有 `students` 属性的状态。
  * `students` 默认值因该是一个空数组.
* 创建一个 `componentDidMount` 方法，用于向 `json-server` 进行 `HTTP` 请求：
  * 安装 `axios` ，并且在组件中 `import` .
  * `json-server` 的API url是 `http://localhost:3005/students?class=`.
    * Class 应该等于 `MATH1010` OR `ENG2010` OR `BIO2020` 之一，取决于路由参数是什么。
    * 提示: `react-router-dom` 向一个组件的 `props` 传递一个 `match` 对象。
  * 使用向API 请求的返回值数据更新 `state` 中的 `students` 数组。
* 找到组件中的 `render` 方法。
* 使用 `map` 遍历 `students` 数组，用 `h3` 标签返回学生的 `first` 和 `last` 姓名。
  * 记住React在mapped元素中需要一个唯一的 `key` 属性。
  * 使用 `first_name` 和 `last_name` 作为特性。
* 在 `h2` 标签下面， 渲染 `mapped` 遍历出的学生。
* 更新 `h1` 标签，用于展示页面的课程名称。
  * 提示: `react-router-dom` 向组件的 `props` 传递一个 `match` 对象。

<details>

<summary> 详细说明 </summary>

<br />

Let's begin by opening `./src/components/ClassList/ClassList.js`. In the `constructor` method, let's initialize `state` to have a property called `students` that equals an empty array. This is where we'll store our returned data from hitting the `json-server`. 

```js
constructor() {
  super();

  this.state = {
    students: []
  };
}
```

Now that we have somewhere to store our API results, let's focus on the code to actually make the API request. First, we'll need `axios`. Let's use `npm install --save axios` to add it to our project and also `import` it at the top of our component. After that, let's create a `componentDidMount` lifecycle method. This will allow us to get our students as soon as possible. 

```js
componentDidMount() {

}
```

Since we are `fetching` data, let's make a `GET` request to the API url: `http://localhost:3005/students?class=` where class equals the current class page. `react-router-dom` automatically passes down a couple handy props into the routeable components. One of them is called `match`. It is an object with a bunch of useful information. One of the properties on `match` is called `params`. This is where we can see the value of any `route parameters`. Our route parameter is called `class`. Therefore, we can access it by using `this.props.match.params.class`. 

That means our `GET` request url should look like: `http://localhost:3005/students?class=${ this.props.match.params.class }`. We can then capture the results of this API request and use `setState` to update the value of `students` to be the result's data.

```js
axios.get(`http://localhost:3005/students?class=${ this.props.match.params.class }`).then( results => {
  this.setState({
    students: results.data
  });
});
```

Now that we have our students coming in from our `json-server`, let's use a `map` in the render method to render each student's `first` and `last` name in a `h3` element. Remember the react requires mapped elements to have a unique `key` property. In this case, we'll just use the `index` of the `map`.

```js
render() {
  const students = this.state.students.map((student, i) => (
    <h3 key={ i }>{ student.first_name } { student.last_name }</h3>
  ));

  return (
    <div className='box'>
      <h1></h1>
      <h2>ClassList:</h2>

    </div>
  )
}
```

We can then use `{ }` to render the `h3` elements under the `h2` element.

```js
render() {
  const students = this.state.students.map((student, i) => (
    <h3 key={ i }>{ student.first_name } { student.last_name }</h3>
  ));

  return (
    <div className='box'>
      <h1></h1>
      <h2>ClassList:</h2>
      { students }
    </div>
  )
}
```

Lastly, we just need to update the `h1` element to display the current class. Just like how we accessed the route parameter for our `axios` request, we can do the same thing here using `{ }` in our JSX.

```js
<h1>{ this.props.match.params.class }</h1>
```

</details>

### 答案

<details>

<summary> <code> ./src/components/ClassList/ClassList </code> </summary>

```js
import React, { Component } from 'react';
import axios from 'axios';

export default class ClassList extends Component {
  constructor() {
    super();

    this.state = {
      students: []
    };
  }

  componentDidMount() {
    axios.get(`http://localhost:3005/students?class=${ this.props.match.params.class }`).then( results => {
      this.setState({
        students: results.data
      });
    });
  }

  render() {
    const students = this.state.students.map((student, i) => (
      <h3 key={ i }>{ student.first_name } { student.last_name }</h3>
    ));

    return (
      <div className='box'>
        <h1>{ this.props.match.params.class }</h1>
        <h2>ClassList:</h2>
        { students }
      </div>
    )
  }
}
```

</details>

<br />

<img src="https://github.com/DevMountain/react-4-afternoon/blob/solution/readme-assets/6g.gif" />

## 步骤 6

### 概括

在这一步中，我们将开始在 `./src/components/Student/Student.js` 组件中设置学生的详细视图。`Student` 组件应该能够渲染所给的的任何学生，为了实现该功能，我们将使用路由参数作为一个学生的ID。

### 操作指引

* 打开 `./src/routes.js`.
* 引入 `Student` 组件作为一条路由。
* 创建一个 `Student` 路由具备以下特性：
  * Path: `/student/:id` - Component: `Student`。
* 打开 `./src/components/ClassList/ClassList.js`。
* 从 `react-router-dom` 引入 `Link` 组件。
* 使用 `Link` 组件包裹 `h3` 标签。
* 给 `Link` 组件设置 `to` 属性 `/student/:id`, 其中 `id` 应该等于学生的ID。
  * 记得将唯一的 `key` 属性移动到map渲染的最外层元素上。

<details>

<summary> 详细说明 </summary>

<br />

Let's begin by opening `./src/routes.js` and `import` the `Student` component at the top of the file with the other components. We'll need to make a new route for this `Student` component that uses an `id` route parameter. Similarly to how we did it with the `ClassList` component, we can use `axios` to fetch a specific student on load by making a match to the `id` property. For example, if `id` equaled `1` we could fetch a student where the `id` equaled `1`. The `path` for this route should be `/student/:id`.

```js
<Route component={ Student } path='/student/:id' />
```

Now that we have our `Student` route setup, let's open the `ClassList` component and `import` the `Link` component from `react-router-dom`. We'll need to update our `map` in the `render` method to wrap the `h3` element in a `Link` component. In this `map`, we have access to all the student's properties. Therefore, if we need the `id`, we can access it by `student.id`. Let's set the `to` prop of the `Link` component to be `/student/${ student.id }`. We'll also need to move the `key` prop onto the `Link` component since it'll now be the most parent item.

```js
const students = this.state.students.map((student, i) => (
  <Link to={`/student/${student.id}`} key={ i }>
    <h3>{ student.first_name } { student.last_name }</h3>
  </Link>
));
```

</details>

### 答案

<details>

<summary> <code> ./src/routes.js </code> </summary>

```js
import React from 'react';
import { Switch, Route } from 'react-router-dom';
import Home from './components/Home/Home';
import About from './components/About/About';
import ClassList from './components/ClassList/ClassList';
import Student from './components/Student/Student';

export default (
  <Switch>
    <Route component={ Home } exact path="/" />
    <Route component={ About } path="/about" />
    <Route component={ ClassList } path='/classlist/:class' />
    <Route component={ Student } path='/student/:id' />
  </Switch>
)
```

</details>

<details>

<summary> <code> ./src/components/ClassList/ClassList.js </code> </summary>

```js
import React, { Component } from 'react';
import { Link } from 'react-router-dom';
import axios from 'axios';

export default class ClassList extends Component {
  constructor() {
    super();

    this.state = {
      students: []
    };
  }

  componentDidMount() {
    axios.get(`http://localhost:3005/students?class=${ this.props.match.params.class }`).then( results => {
      this.setState({
        students: results.data
      });
    });
  }

  render() {
    const students = this.state.students.map((student, i) => (
      <Link to={`/student/${student.id}`} key={ i }>
        <h3>{ student.first_name } { student.last_name }</h3>
      </Link>
    ));

    return (
      <div className='box'>
        <h1>{ this.props.match.params.class }</h1>
        <h2>ClassList:</h2>
        { students }
      </div>
    )
  }
}
```

</details>

<br />

<b>当页面间导航变化时观察URL的变化</b>

<img src="https://github.com/DevMountain/react-4-afternoon/blob/solution/readme-assets/7g.gif" />

## 步骤 7

### 概括

在这一步中，我们将更新 `Student` 组件，以展示一个具体学生的信息，为了得到这个信息，我们将查询路由参数中的 `id`，然后用它结合 `axios` 的 `HTTP` 请求从我们的 `json-server` 中获取数据。

### 操作指引

* 打开 `src/components/Student/Student.js`.
* 创建一个构造方法 `constructor` ，初始化一个名为 `studentInfo` 的状态。
  * `studentInfo` 默认值应该是一个空对象。
* 创建一个`componentDidMount` 方法，用于向 `json-server` 进行 `HTTP` 请求：
  * 在组件中引入 `axios` 。
  *  `json-server`  API url 为 `http://localhost:3005/students/ID_GOES_HERE`。
       * `ID_GOES_HERE` 应该等于学生的 id。
       * 提示: `react-router-dom` 向组件 `props` 传递一个 `match` 对象。
  * 使用从API中返回的数据更新状态中的 `studentInfo` 对象。
* 找到组件中的 `render` 方法。
* 在 `h1` 标签下面, 展示状态中 `studentInfo` 的特性:
  * 将`first_name` 和 `last_name` 写在一个 `h1` 标签中。
  * 文字 `Grade:` 后面紧跟 `grade` 特性，将其写在一个 `h3` 标签中。
  * 文字 `Email:` 后面紧跟 `email` 特性，将其写在一个 `h3` 标签中。

<details>

<summary> 详细说明 </summary>

<br />

Let's begin by opening `src/components/Student/Student.js` and import `axios` at the top of the file with the other imports. We'll need a place to store our data from hitting the API, let's update the constructor method to have a property called `studentInfo` that defaults to an empty object.

```js
constructor() {
  super();

  this.state = {
    studentInfo: {}
  };
}
```

Now that we have somewhere to store the data, let's create a `componentDidMount` method. Inside this method let's use `axios` to make a `GET` request to `http://localhost:3005/students/ID_GOES_HERE`. Similarly to `ClassList`, we can access the `id` for the given student on the `match` object that `react-router-dom` passes into our routeable components. Therefore, our API url would look like: `http://localhost:3005/students/${this.props.match.params.id}`. Let's capture the results of this `GET` request and use the data to update the value of `studentInfo` on `state`.

```js
componentDidMount() {
  return axios.get(`http://localhost:3005/students/${this.props.match.params.id}`).then( results => {
    this.setState({
      studentInfo: results.data
    });
  });
}
```

Now that we have the student data coming in, we can go into the render method and display the pieces of the student's information. Let's put the student's `first_name` and `last_name` within a `h1` tag and let's put the grade and email in their own `h3` tags.

```js
render() {
  return (
    <div className='box'>
      <h1>Student:</h1>
      <h1>{this.state.studentInfo.first_name} {this.state.studentInfo.last_name}</h1>
      <h3>Grade: {this.state.studentInfo.grade}</h3>
      <h3>Email: {this.state.studentInfo.email}</h3>
    </div>
  )
}
```

</details>

### 答案

<details>

<summary> <code> ./src/components/Student/Student.js </code> </summary>

```js
import React, { Component } from 'react';
import axios from 'axios';

export default class Student extends Component {
  constructor() {
    super();

    this.state = {
      studentInfo: {}
    };
  }

  componentDidMount() {
    return axios.get(`http://localhost:3005/students/${this.props.match.params.id}`).then( results => {
      this.setState({
        studentInfo: results.data
      });
    });
  }
    
  render() {
    return (
      <div className='box'>
        <h1>Student:</h1>
        <h1>{this.state.studentInfo.first_name} {this.state.studentInfo.last_name}</h1>
        <h3>Grade: {this.state.studentInfo.grade}</h3>
        <h3>Email: {this.state.studentInfo.email}</h3>
      </div>
    )
  }
}
```

</details>

<br />

<img src="https://github.com/DevMountain/react-4-afternoon/blob/solution/readme-assets/8g.gif" />

## 步骤 8

### 概括

在这一步中，我们将添加一个导航栏，用于联系 `About`, `History`, 和 `Contact` 组件。

### 操作指引

* 打开 `src/components/About/About.js`。
* 从 `react-router-dom` 中引入 `Link` 组件。
* 在含有className `subnav` 的 `div` 中，添加3个 `h3` 标签，标签中写入以下文字：
  * `About`
  * `History`
  * `Contact`
* 用包含以下路径的 `Link` 组件包裹 `h3` 标签：
  * About - `/about`
  * History - `/about/history`
  * Contact - `/about/contact`
* 给每个 `Link` 组件设置类名 className 为 `subnav_links`.

### 答案

<details>

<summary> <code> ./src/components/About/About.js </code> </summary>

```js
import React, { Component } from 'react';
import { Link } from 'react-router-dom';

export default class About extends Component {
  render() {
    return (
      <div>
        <div className='subnav'>
          <Link to='/about' className='subnav_links'><h3>About</h3></Link>
          <Link to='/about/history' className='subnav_links'><h3>History</h3></Link>
          <Link to='/about/contact' className='subnav_links'><h3>Contact</h3></Link>
        </div>
        <div className='box'>
        </div>
      </div>
    )
  }
} 
```

</details>

<img src="https://github.com/DevMountain/react-4-afternoon/blob/solution/readme-assets/9.png" />

## 步骤 9

### 概括

在这一步中，我们将为`About`, `History`, 和 `Contact` 组件创建子路由。在这一步中，我们将避免使用过于详细的提示，给你一些小小的挑战。用你在前面步骤中学到的知识完成它。如果陷入困境，你可以查看答案。

### 操作指引

* 打开 `src/components/About/About.js`。
* 从 `react-router-dom` 中引入 `Switch` 和 `Route`。
* 引入 `History` 和 `Contact` 组件。
* 在className为 `box` 的 `div` 标签中 , 添加一个 `Switch` 组件。
* 在 `Switch` 组件中添加3个路由：
  * 第一个和第二个路由应该分别指向 `History` 和 `Contact` 组件。
    * 提示： 对于这些组件的路径应该和 `Link` 组件的 `to` 属性使用相同的值。
  * 第三个路由应该在路径为 `/about`的<b>exact</b> 渲染 `JSX` ( 而不是一个组件 )  。
  * 为了渲染JSX而不是一个组件，你可以使用一个相当于一个返回JSX的函数的 `render` 属性。
    * <details>
      
      <summary> <code> 关于 JSX </code> </summary>
      
      ```html
      <div>
        <h1 className='title'>About WestSide University:</h1>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed euismod eu lorem et ultricies. In porta lorem at dui semper porttitor. Nullam quis cursus dui. Cras tincidunt vehicula tellus eu facilisis. Donec nisi turpis, iaculis et arcu a, aliquet ultrices nisl. Nam in pharetra odio, ac blandit metus. Suspendisse potenti. Praesent elementum diam non orci cursus rutrum. Pellentesque condimentum ultrices dignissim. Sed a tempor ligula, vel luctus sapien. Mauris vehicula rutrum massa. Duis condimentum, ex quis ullamcorper rhoncus, erat libero tempor arcu, condimentum facilisis tellus lectus ut nunc. Pellentesque vitae faucibus diam. Vestibulum eu erat ex. Ut justo neque, varius aliquet erat vel, scelerisque convallis lacus. Mauris semper lorem mauris, sed dignissim eros consectetur nec.
        </p>
      </div>
      ```
      
      </details>

### 答案

<details>

<summary> <code> ./src/components/About/About.js </code> </summary>

```js
import React, { Component } from 'react';
import { Switch, Route, Link } from 'react-router-dom';
import History from '../History/History';
import Contact from '../Contact/Contact';

export default class About extends Component {
  render() {
      return (
        <div>
          <div className='subnav'>
            <Link to='/about' className='subnav_links'><h3>About</h3></Link>
            <Link to='/about/history' className='subnav_links'><h3>History</h3></Link>
            <Link to='/about/contact' className='subnav_links'><h3>Contact</h3></Link>
          </div>

          <div className='box'>
            <Switch>
              <Route path='/about/history' component={ History }/>
              <Route path='/about/contact' component={ Contact }/>
              <Route path='/about' render={() => (
                <div>
                    <h1>About the University</h1>
                    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed euismod eu lorem et ultricies. In porta lorem at dui semper porttitor. Nullam quis cursus dui. Cras tincidunt vehicula tellus eu facilisis. Donec nisi turpis, iaculis et arcu a, aliquet ultrices nisl. Nam in pharetra odio, ac blandit metus. Suspendisse potenti. Praesent elementum diam non orci cursus rutrum. Pellentesque condimentum ultrices dignissim. Sed a tempor ligula, vel luctus sapien. Mauris vehicula rutrum massa. Duis condimentum, ex quis ullamcorper rhoncus, erat libero tempor arcu, condimentum facilisis tellus lectus ut nunc. Pellentesque vitae faucibus diam. Vestibulum eu erat ex. Ut justo neque, varius aliquet erat vel, scelerisque convallis lacus. Mauris semper lorem mauris, sed dignissim eros consectetur nec.</p>
                </div>
              )}/>
            </Switch>
          </div>
        </div>
      )
  }
}
```

</details>

<br />

<img src="https://github.com/DevMountain/react-4-afternoon/blob/solution/readme-assets/10g.gif" />

## 进阶

尝试在学生详情页 `Student` 添加一个路由返回课程列表页 `ClassList` 的返回按钮。你也可以在课程课程列表页 `ClassList` 添加一个路由返回到首页 `Home` 的按钮。

## 贡献

如果你发现一个问题或者有文字错误，请fork我们的代码仓库，进行必要的修改并进行提交，我们才能审核你的修改，并将它合并到master repo 和 master分支上。

## 版权

© DevMountain LLC, 2017. Unauthorized use and/or duplication of this material without express and written permission from DevMountain, LLC is strictly prohibited. Excerpts and links may be used, provided that full and clear credit is given to DevMountain with appropriate and specific direction to the original content.

<p align="center">
<img src="https://s3.amazonaws.com/devmountain/readme-logo.png" width="250">
</p>
