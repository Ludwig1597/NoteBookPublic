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
    <!-- 准备好一个容器 -->
    <div id="test"></div>

    <!-- 引入react核心库,全局多了一个对象：React -->
    <script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
    <!-- 引入react-dom,用于支持react操作dom，全局多了一个对象: ReactDOM -->
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>
    <!-- 引入babel，用于将jsx转化为js -->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <!-- 引入prop-types.用于对组件标签属性进行限制, 全局多了一个对象：PropTypes -->
    <script src="https://cdn.bootcss.com/prop-types/15.6.1/prop-types.js"></script>
    
    <script type="text/babel">
        //组件内的标签可以定义ref属性来标识自己
        //创建组件
        class Demo extends React.Component{
 
            //展示左侧输入框的数据
            showData = ()=>{
                //给标签加一个id
                //const input=document.getElementById("input1");
                //alert(input.value);
                console.log(this.refs.input1); 
                const {input1} = this.refs;
                alert(input1.value);
            }

            //展示右侧输入框的数据
            showData2 = ()=>{
                const {input2} = this.refs;
                alert(input2.value);
            }

            render(){
                return (
                    <div>
                        <input ref="input1" type="text" placeholder="点击按钮提示数据"/>&nbsp;
                        <button onClick={this.showData}>点我左侧的框</button>&nbsp;
                        <input ref="input2" onBlur={this.showData2} type="text" placeholder="失去焦点提示数据"/>
                    </div>
                )
            }
        }
        
        //渲染组件
        ReactDOM.render(<Demo />,document.getElementById("test"));
    </script>
</body>

</html>
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU3NTA1NjAxNV19
-->