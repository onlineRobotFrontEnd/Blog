
---
title: React Hooks分享
author: zhangqing
date: 2019-12-12
---

# React Hooks分享  
## React hooks是什么  
<!--more-->

1、类组件  
`class Counter extends Component{
render(){  
               return “hello world”
                   }  
            }  `  
类组件的优点：  
拥有state状态  
1. 需要生命周期函数  
2. 需要副作用操作  
3. 函数组件  
`const Counter=()=>{  
        return “hello world”
}  `  
2、函数式优点：  
*  简单易懂  
*  符合UI=f（state）的原则  
*  函数式编程  

react Hooks 是一些可以让你在函数组件里“钩入” React state 及生命周期等特性的函数  
React hooks官网：https://zh-hans.reactjs.org/docs/hooks-intro.html  
![对比](/Blog/images/assets/1.png)
### 一、useState介绍  
useState返回的值：  
const [count,setCount]=useState(0);  
const [属性, 操作属性的方法] = useState(默认值);  
相当于一个解构：  
`     const state=useState(0);   
          const count=state[0];  
    const setCount=state[1];`


![对比](/Blog/images/assets/2.png)
useState返回结果可以任意取名，useState可以多个使用  
使用useState规则： Hook 在每次渲染时都按照相同的顺序被调用  
那么 React 怎么知道哪个 state 对应哪个 useState？  
答案是 React 靠的是 Hook 调用的顺序。因为我们的示例中，Hook 的调用顺序在每次渲染中都是相同的，所以它能够正常工作 
![对比](/Blog/images/assets/66.png)
结论：不要在循环，条件或嵌套函数中调用 Hook， 确保总是在你的 React 函数的最顶层调用他们 
![对比](/Blog/images/assets/10.png)
使用Hook的规则：  
1、只在最顶层使用 Hook  
2、在 React 的函数组件中调用 Hook  
3、在自定义 Hook 中调用其他 Hook遵循此规则  
3、不要在普通的 JavaScript 函数和React class组件中调用 Hook  
4、自定义hook，假设任何以 「use」 开头并紧跟着一个大写字母的函数就是一个 Hook，以便于react辨别函数内部可以调用其他的 Hook
![对比](/Blog/images/assets/6.png)
![对比](/Blog/images/assets/4.png)
state永远都是新的值
这一点同我们过去class组件中的state是完全不一样的。在class组件中，state一直是挂载在当前实例下，保持着同一个引用。  
而在函数式组件中，没有this。  
不管你的state是一个基本数据类型（如string、number），还是一个引用数据类型（如object），只要是通过useState获取的state，每一次render，都是新的值。 useState返回的状态更新方法，只是让下一次render时的state能获取到当前最新的值。而不是保持一个引用、更新那个引用值。

### 二、useEffect介绍  
useEffect可以让你在函数组件中执行副作用操作：在 React 更新 DOM 之后运行一些额外的代码。比如发送网络请求，手动变更 DOM，事件监听，定时器……  
useEffect 在渲染结束时执行，所以不会阻塞浏览器渲染进程  
useEffect = componentDidMount  +   componentDidUpdate  +  componentWillUnmount ；  
useEffect可以在一个组件中写多个，按顺序执行

useEffect 模拟 componentDidMount 和 componentWillUnmount  
`useEffect (()  =>  {     
    	//  只有DidMount调用这里  
        	return ()  =>  {  	       
                 //  只有unmount的时候走这里  
                 	}  
                     },  [])；`  
Didmount：如果想执行只运行一次的 effect（仅在组件挂载和卸载时执行），可以传递一个空数组（[]）作为第二个参数。这就告诉 React 你的 effect 不依赖于 props 或 state 中的任何值，所以它永远都不需要重复执行  
Unmount: effect 中return是 effect 可选的清除机制。每个 effect 都可以返回一个清除函数。如此可以将添加和移除订阅的逻辑放在一起。它们都属于 effect 的一部分  

useEffect 模拟 componentDidUpdate  
useEffect 会在每次渲染后都执行在第一次渲染之后和每次更新之后都会执行。去掉首次渲染就可以实现  
componentDidUpdate  
const mounted = useRef();  
useEffect(()  =>  {  
         if  (!mounted.current)  {   
                mounted.current = true;  
                }  else  {  
                    	// do componentDidUpdate       }  
                        })  
因为useEffect 会在每次渲染后都执行，因此需要通过 useEffect 的第二个参数告诉 React 用到了哪些外部变量（第二个参数不是必须的）  
第二个参数[param1,param2,param3,…]是或的关系，只要其中一个改变就触发更新

因此需要开发者通过 useEffect 的第二个参数告诉 React 用到了哪些外部变量  
而是effect本应该每次render都触发，但因为effect内部依赖了外部数据，外部数据不变则内部effect执行无意义。因此只有当外部数据变更时，effect才会重新触发。  
useEffect规则：只要内部使用了某个外部变量，函数也好、变量也好，都应该填写到依赖配置中
useEffect的优势：  
Class组件中是按照生命周期写逻辑componentDidMount 和 componentDidUpdate，componentWillUnmount
你可以使用多个 effect，将不相关逻辑分离到不同的 effect 

### 三、useLayoutEffect介绍  
useLayoutEffect在浏览器重新绘制页面布局前  
useLayoutEffect内部的更新将会同步刷新  
useLayoutEffect 可以看作是 useEffect 的同步版本，但是不同的是：  
1、useEffect，使用useEffect不会阻塞浏览器的重绘  
2、useLayoutEffect, 使用useLayoutEffect，会阻塞浏览器的重绘。如果你需要手动的修改Dom，推荐使用useLayoutEffect。因为如果在useEffect中更新Dom，useEffect不会阻塞重绘，用户可能会看到因为更新导致的闪烁  
3、因为 useLayoutEffect 是同步的，如果我们要在 useLayoutEffect 调用状态更新，或者执行一些非常耗时的计算，可能会导致 React 运行时间过长，阻塞了浏览器的渲染
![对比](/Blog/images/assets/16.png)

### 四、useContext介绍  
useContext的使用：可访问全局状态，避免一层层的传递状态。   
` 
const ThemeContext = React.createContext('light');  
<ThemeContext.Provider value={theme}>  
      <AppMiddle onClick={toggleTheme} />
</ThemeContext.Provider>  `  
Hooks之前的写法：  
`<ThemeContext.Consumer>  
{theme  => (<div>{theme}</div>)}
</ThemeContext.Consumer>  `  
Hooks之后的写法  
 `const theme = useContext(ThemeContext);<div>{theme}</div>`  

### 五、useRef介绍  
 useRef：  `const refContainer = useRef(initialValue);`  
useRef 返回一个可变的 ref { current: initValue } 对象，其 .current 属性被初始化为传递的参数（initialValue）。该对象在整个生命周期中保持不变。   
从本质上讲，useRef就像一个“盒子”，可以在其.current财产中保持一个可变的价值。  
useRef() Hooks 不仅适用于 DOM 引用。 “ref” 对象是一个通用容器，其 current 属性是可变的，可以保存任何值（可以是元素、对象、基本类型、甚至函数），类似于类上的实例属性。  


useRef 主要有两个使用场景：  
1、获取子组件或者 DOM 节点的句柄  
2、渲染周期之间的共享数据的存储  
使用场景：获取上一轮的 props 或 state 
通过 useEffect 在组件渲染完毕后再执行的特性，再利用 useRef 的可变特性，让 usePrevious 的返回值是 “上一次” Render 时的值  
`function usePrevious(value)  {   
      const ref = useRef();  
      useEffect(() => {  
 	ref.current = value;   
       });  
      return ref.current;  
 }  `  

 ### 六、useCallback介绍  
 useCallback都会在组件第一次渲染的时候执行，之后会在其依赖的变量发生改变时再次执行，useCallback返回缓存inline函数。防止因属性更新时生成新的函数导致子组件重复渲染  
useCallback接受函数和一个数组输入，并返回的一个缓存版本的回调函数，仅当重新渲染时数组中的值发生改变时，才会返回新的函数实例，这也就解决我们上面提到的优化子组件性能的问题，并且也不会有上面繁琐的步骤。
返回值为 回调函数，第一个参数为一个函数，第二个为一个数组，只有内部元素变化，返回的回调函数才会被重新创建  
`componentDidUpdate(prevProps) {  
      if ( this.props.count   !==  prevProps.count && 		this.props.step !== prevProps.step) { 
	this.props.fetchData();   
      }  
 }`  
useCallback(callback: T, deps: DependencyList): callback  
把内联回调函数及依赖项数组作为参数传入 useCallback，它将返回该回调函数的 memoized 版本，该回调函数仅在某个依赖项改变时才会更新。当你把回调函数传递给经过优化的并使用引用相等性去避免非必要渲染（例如 shouldComponentUpdate）的子组件时，它将非常有用。  

### 七、React.memo介绍  
在 Fucntion Component 中，React.memo 等效于 PureComponent，浅比较 props。  
用 memo 做 PureRender   ===  函数组件中的shouldComponentUpdate:  
`const Child = memo((props) => {   
     return    ……
 }, (nextProps, prevProps) => {   
       // 做我们想做的事情，类似shouldComponentUpdate   
})  `  

使用 memo 包裹的组件，会在自身重渲染时，对每一个 props 项进行浅对比，如果引用没有变化，就不会触发重渲染。  

### 八、useMemo介绍  
`const a = useMemo(() => memorizeValue, deps) `

useMemo返回缓存数据和计算结果。  
用 useMemo 做局部 PureRender
useMemo返回的是一个缓存的值。  
也就是仅当重新渲染时数组中的值发生改变时，回调函数才会重新计算缓存数据，这可以使得我们避免在每次重新渲染时都进行复杂的数据计算。因此我们可以认为:
useCallback(fn, input) 等同于 useMemo(() => fn, input)  
如果没有给useMemo传入第二个参数，则useMemo仅会在收到新的函数实例时，才重新计算，需要注意的是，React官方文档提示我们，useMemo仅可以作为一种优化性能的手段，不能当做语义上的保证，这就是说，也会React在某些情况下，即使数组中的数据未发生改变，也会重新执行。
Hooks性能
在现代浏览器中，与类相比，闭包的原始性能没有显著差异，除了在极端情况下。 此外，考虑到Hooks的设计在以下几个方面更有效：  
1、钩子避免了类所需的大量开销，例如在构造函数中创建类实例和绑定事件处理程序的成本。  
2、使用Hooks的惯用代码不需要深层组件树嵌套，这在使用高阶组件，渲染道具和上下文的代码库中很常见。 使用较小的组件树，React的工作量较少。  
Hooks优势  
1、方便复用状态逻辑  
2、副作用的关注点分离  
3、函数组件无 this 问题  
![对比](/Blog/images/assets/21.png)
![对比](/Blog/images/assets/22.png)

### 九、useReducer  
useReducer主要用于更新复杂逻辑的状态  
useReducers可以传入三个参数，第一个参数就是形如(state,action) => newState这样的reducer，第二参数是初始化默认值，第三个参数是一个函数，接受第二个参数进行计算获取默认值(可选)。  
seReducer接收三个参数，reducer函数，initialArg初始值，init惰性初始值函数。reducer函数和Redux的reducer类似，接收state，以及action。返回更新后的state。如果传入三个参数，init(initialArg)将作为初始值。  
useReducer在复杂场景下比useState更适用。  
指定初始state  
useReducer的第二个参数可以指定初始的state  
惰性初始化  
如果指定useReducer的第三个参数，useReducer的初始值会被设置为init(initialArg)  
React 会确保 dispatch 函数的标识是稳定的，并且不会在组件重新渲染时改变。  
![对比](/Blog/images/assets/24.png)
