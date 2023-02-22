### 生命周期
#### 旧
1.初始化阶段：由ReactDOM.render()触发--初次渲染

1. constructor()
2. compoentWillMount()
3. render()
4. componentDidMount()

2.更新阶段:有组件内部this.setState()或父组件重新render触发

1. shouldComponentUpdate()
2. componentWillUpdata()
3. render()
4. componentDidUpdate()

3.卸载组件:由ReactDOM.unmountComponentAtNode()触发

1. componentWillUnmount

#### 新
1. 初始化阶段：由ReactDOM.render()触发--初次渲染
2. getDerivedStateFromProps
3. render()
4. componentDidMount()

2.更新阶段：有组件内部this.setState()或父组件重新render()触发
1. getDerivedStateFromProps
2. shouldComponentUpdate()
3. render()
4. getSnapshotBeforeUpdate
5. componentDidUpdate()

3.卸载组件：由ReactDOM.unmountComponentAtNode()触发

1. componentWillUnmount()

### 路由的基本使用		
```js
import {BrowserRouter,Link,Routes, Route} from 'react-router-dom'
import Home from './pages/Layout'
function App(){
	return(
	 <BrowserRouter>
		<div className="App">
		<Link to="/home" className="link">首页 </Link>
		<Routes>  
			    <Route path="/home" element={<Home/>}></Route>  
		  </Routes>
		</div>
	 </BrowserRouter>
	);
}
```
### 导入本地图片的方法
```js
import logo from '../../asstes/logo.png';
<img src={logo} alt=""/>
```
### jsx语法规则
1.定义虚拟DOM时，不要写引号
2.标签中混入JS表达式时要用{}
3.样式的类名指定不要用class，要用className
4.内联样式，要用style={{key:value}}的形式去写
5.虚拟DOM必须只有一个根标签
### 函数式组件
1.首字母必须大写