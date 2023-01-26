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
    <div id="test1"></div>
    <div id="test2"></div>
    <div id="test3"></div>
    <!-- 引入react核心库 -->
    <script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
    <!-- 引入react-dom,用于支持react操作dom -->
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>
    <!-- 引入babel，用于将jsx转化为js -->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script type="text/babel">
        //props解决了外部向组件传参数
        //1. 创建组件
        class Person extends React.Component{
            render(){
                console.log(this)
                const {name,sex,age}=this.props
                return (
                    <ul>
                        <li>姓名: {name}</li>
                        <li>性别: {sex}</li>
                        <li>年龄: {age}</li>
                    </ul>
                )
            }
        }

        //2. 渲染组件到页面
        ReactDOM.render(<Person name="tom" age="18" sex="女"/>,document.getElementById("test1"));
        ReactDOM.render(<Person name="jerry" age="19" sex="男"/>,document.getElementById("test2"));

        const p={name:"mike",age:22,sex:"男"}
        //ReactDOM.render(<Person name={p.name} age={p.age} sex={p.sex}/>,document.getElementById("test3"));
        ReactDOM.render(<Person {...p} />,document.getElementById("test3"));//批量传递标签属性（批量传递props）
    </script>
</body>

</html>
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk2MjcwNjY1XX0=
-->