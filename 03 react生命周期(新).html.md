<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .title {
            background-color: orange;
            widows: 200px;
        }
    </style>
</head>

<body>
    <div id="test"></div>
    <script type="text/javascript" src="./../99 react17/react.development.js"></script>
    <script type="text/javascript" src="./../99 react17/react-dom.development.js"></script>
    <script type="text/javascript" src="./../99 react17/babel.min.js"></script>
    <script type="text/javascript" src="./../99 react17/prop-types.js"></script>
    
    <script type="text/babel">
        class Count extends React.Component{
            //构造器
            constructor(props){
                console.log('Count-constructor');
                super(props)
                //初始化状态
                this.state={number: 0}
            }
            
            //按钮的回调
            add=()=>{
                const {number}=this.state;
                this.setState({
                    number:number+1
                })
            }
            //卸载组件按钮的回调
            death=()=>{
                ReactDOM.unmountComponentAtNode(document.getElementById('test'))
            }
            //强制更新按钮的回调
            force=()=>{
                this.forceUpdate()
            }
            //此方法适用于罕见的用例，即state的值任何时候都取决于props
            //派生状态会导致代码冗余，并且使组件难以维护
            static getDerivedStateFromProps(props,state){
                console.log('Count-getDerivedStateFromProps',props,state)
                //return props;
                return null;
            }
            //在更新之前获取快照（此用法并不常见）
            getSnapshotBeforeUpdate(){
                console.log('Count-getSnapshotBeforeUpdate');
                return "atsamsung";
            }
            //组件挂载完毕的钩子
            componentDidMount(){
                console.log('Count-componentDidMount');
            }
            //组件将要卸载的钩子
            componentWillUnmount(){
                console.log('Count-componentWillUnmount');
            }
            //控制组件更新的“阀门”
            shouldComponentUpdate(){
                console.log('Count-shouldComponentUpdate');
                if(this.state.number%2==0)
                    return false;
                return true;
            }
            //组件更新完毕的钩子
            componentDidUpdate(preProps,preState,snapshotValue){
                console.log('Count-componentDidUpdate',preProps,preState,snapshotValue);
            }
            render(){
                console.log('Count-render');
                return (
                    <div>
                        <h2>当前求和为：{this.state.number}</h2>
                        <button onClick={this.add}>点我+1</button>
                        <button onClick={this.death}>卸载组件</button>
                        <button onClick={this.force}>不更改任何状态中的数据，强制更新一下</button>
                    </div>
                )
            }
        }
        
        //渲染组件到页面 
        ReactDOM.render(<Count number={199}/>,document.getElementById('test'));
    </script>
</body>

</html>
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk4OTQzODE5OF19
-->