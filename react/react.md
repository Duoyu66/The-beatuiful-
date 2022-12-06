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
