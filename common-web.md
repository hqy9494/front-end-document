# 后台系统简易教程
[项目地址common-web](https://git.yoopin.com.cn/common/common-web.git)

## 一：项目目录（src）
- assets 资源文件
- boot项目入口
- common权限配置
- components组件
- config项目配置
- containers配置页面
- pages页面
- services中间件（请求、登陆等）
- styles公共全局样式
- utils工具类
- routers.js路由配置

## 二：添加页面
流程：
1. 添加路由(routers.js) 
2. 添加页面配置文件(containers) 
    1. 在相应的目录下添加相应的页面配置文件
    2. 把配置文件暴露给路由
3. 添加页面文件(pages) 
    1. 添加页面文件
    2. 暴露页面文件给路由

### 2.1：添加路由
```javascript
// routers.js
home: {
  module: "",
  path: "/",
  redirect: "/dashboard",
  subs: {
    //主页
    Index: {
      path: "Index",
      module: "Index",
      component: "Index",
      title: "主页"
    }
  }
}
```

### 2.2：添加页面配置文件(containers) 
在src/containers下创建Index/index.js和Index/modules.js

```javascript
// Index/index.js
export default {
  initialState: {
    title: "主 页",
    // subTitle: [{ display: "主 页" }],
    selectedKeys: "index",
    openKeys: "index"
  },
  component: [
    {
      module: "Index",
      getProps: ["rts"]
    }
  ]
}

```

```javascript
// Index/modules.js
import Index from "./Index";

export default {
  Index
};
```

然后暴露给路由，在src/containers/Main/makeRouters.js下添加
```javascript
import Index from "../Index/modules";

const modules = {
  Index,
}
```

### 2.3：添加页面文件(pages)
在src/page目录下创建Index/index.js

```javascript
import React from "react";
import { connect } from "react-redux";
import { createStructuredSelector } from "reselect";
import uuid from "uuid";

export class Index extends React.Component {
  constructor(props) {
    super(props);
    this.state = {};
    this.uuid = uuid.v1();
  }

  componentWillMount() {}

  componentWillReceiveProps(nextProps) {}

  return (
    <section className="index-page">首页</section>
  )
}

const mapDispatchToProps = dispatch => {
  return {};
};

const mapStateToProps = createStructuredSelector({
  UUid: state => state.get("rts").get("uuid")
});

export default connect(mapStateToProps, mapDispatchToProps)(Index)

```

把页面暴露给路由
```javascript
import Index from "./Indexs/Index";

export default {
  Index,
}
```

最后就可以在http://xxx/#/Index下访问你的页面

## 三：数据获取
流程：
1. 在资源加载完后调用rts方法
2. 添加需要监听的请求数据
3. 判断请求数据是否获取成功，如果成功把请求数据添加到当前的状态(state)中
4. 把当前状态的数据渲染在视图中

### 3.1 调用rts
```javascript
export class Index extends React.Component {
  constructor(props) {
    super(props);
    this.state = {};
    this.uuid = uuid.v1();
  }

  componentDidMount() {
    this.get()
  }

  componentWillReceiveProps(nextProps) {}

  get = () => {
    this.props.rts({
      method: 'get',
      url: '/index'
    }, this.uuid, 'getCat')
  }

  return (
    <section className="index-page">首页</section>
  )
}

const mapDispatchToProps = dispatch => {
  return {};
};

const mapStateToProps = createStructuredSelector({
  UUid: state => state.get("rts").get("uuid")
});

export default connect(mapStateToProps, mapDispatchToProps)(Index)
```

### 3.2 监听的请求数据
```javascript
export class Index extends React.Component {
  constructor(props) {
    super(props);
    this.state = {};
    this.uuid = uuid.v1();
  }

  componentDidMount() {
    this.get()
  }

  componentWillReceiveProps(nextProps) {}

  get = () => {
    this.props.rts({
      method: 'get',
      url: '/index'
    }, this.uuid, 'getCat')
  }

  return (
    <section className="index-page">首页</section>
  )
}

const mapDispatchToProps = dispatch => {
  return {};
};

const mapStateToProps = createStructuredSelector({
  UUid: state => state.get("rts").get("uuid"),
  getCat: state => state.get("rts").get("getCat"),
});

export default connect(mapStateToProps, mapDispatchToProps)(Index)
```

### 3.3 成功获取数据后添加到当前状态中
```javascript
export class Index extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      data: []
    };
    this.uuid = uuid.v1();
  }

  componentDidMount() {
    this.get()
  }

  componentWillReceiveProps(nextProps) {
    const { getCat } = nextProps

    if(getCat && getCat[this.uuid]){
      this.setState({
        data: getCat[this.uuid],
      })
    }
  }

  get = () => {
    this.props.rts({
      method: 'get',
      url: '/index'
    }, this.uuid, 'getCat')
  }

  return (
    <section className="index-page">首页</section>
  )
}

const mapDispatchToProps = dispatch => {
  return {};
};

const mapStateToProps = createStructuredSelector({
  UUid: state => state.get("rts").get("uuid"),
  getCat: state => state.get("rts").get("getCat"),
});

export default connect(mapStateToProps, mapDispatchToProps)(Index)
```

### 3.4 把当前状态的数据渲染在视图中
```javascript
export class Index extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      data: []
    };
    this.uuid = uuid.v1();
  }

  componentDidMount() {
    this.get()
  }

  componentWillReceiveProps(nextProps) {
    const { getCat } = nextProps

    if(getCat && getCat[this.uuid]){
      this.setState({
        data: getCat[this.uuid],
      })
    }
  }

  get = () => {
    this.props.rts({
      method: 'get',
      url: '/index'
    }, this.uuid, 'getCat')
  }

  render() {
    const { data } = this.state
    return (
      <section className="index-page">
        {
          data && data.map((v, i) => (
            <div key={i}>{v}</div>
          ))
        }
      </section>
    )
  }
}

const mapDispatchToProps = dispatch => {
  return {};
};

const mapStateToProps = createStructuredSelector({
  UUid: state => state.get("rts").get("uuid"),
  getCat: state => state.get("rts").get("getCat"),
});

export default connect(mapStateToProps, mapDispatchToProps)(Index)
```