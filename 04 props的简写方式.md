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
    <!-- 引入react核心库,全局多了一个对象：React -->
    <script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
    <!-- 引入react-dom,用于支持react操作dom，全局多了一个对象: ReactDOM -->
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>
    <!-- 引入babel，用于将jsx转化为js -->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <!-- 引入prop-types.用于对组件标签属性进行限制, 全局多了一个对象：PropTypes -->
    <script src="https://cdn.bootcss.com/prop-types/15.6.1/prop-types.js"></script>
    <script type="text/babel">
        //创建组件
        class Person extends React.Component {
            //对标签属性进行类型、必要性的限制
            static propTypes = {
                name: PropTypes.string.isRequired,//限制name必传，且为字符串
                sex: PropTypes.string,//限制sex为字符串
                age: PropTypes.number,//限制age为数字
                speak: PropTypes.func//限制speak为函数
            }

            //指定默认标签属性
            static defaultProps = {
                sex: '男',//限制sex默认值为男
                age: 18//限制age默认值为18
            }
            
            render() {
                const { name, sex, age } = this.props
                //props是只读的
                //this.props.name="jack";//报错 因为props是只读的
                return (
                    <ul>
                        <li>姓名: {name}</li>
                        <li>性别: {sex}</li>
                        <li>年龄: {age + 1}</li>
                    </ul>
                )
            }
        }

        //渲染组件到页面
        ReactDOM.render(<Person name="tom" speak={speak} age={18} sex="女" />, document.getElementById("test1"));
        ReactDOM.render(<Person name="jerry" age={19} />, document.getElementById("test2"));

        const p = { name: "mike", sex: "男" }
        //ReactDOM.render(<Person name={p.name} age={p.age} sex={p.sex}/>,document.getElementById("test3"));
        ReactDOM.render(<Person {...p} />, document.getElementById("test3"));//批量传递标签属性（批量传递props）

        function speak() {
            console.log("I am speaking");
        }
    </script>
</body>

</html>
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgxMDM4NjI5Nl19
-->