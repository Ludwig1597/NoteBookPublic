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
        //创建类式组件
        /*
        class Person extends React.Component {
            //对标签属性进行类型、必要性的限制
            static propTypes = {
                name: PropTypes.string.isRequired,
                sex: PropTypes.string,
                age: PropTypes.number,
                speak: PropTypes.func
            }

            //指定默认标签属性
            static defaultProps = {
                sex: '男',
                age: 18
            }
            
            render() {
                const { name, sex, age } = this.props
                return (
                    <ul>
                        <li>姓名: {name}</li>
                        <li>性别: {sex}</li>
                        <li>年龄: {age + 1}</li>
                    </ul>
                )
            }
        }
        */
        
        //创建函数式组件
        function Person(props){
            console.log(this);//undefined
            console.log(props);
            const {name,sex,age}=props;
            return (
                <ul>
                    <li>姓名: {name}</li>
                    <li>性别: {sex}</li>
                    <li>年龄: {age}</li>
                </ul>
            )
        }

        //对标签属性进行类型、必要性的限制
        Person.propTypes = {
            name: PropTypes.string.isRequired,
            sex: PropTypes.string,
            age: PropTypes.number,
            speak: PropTypes.func
        }

        //指定默认标签属性
        Person.defaultProps = {
            sex: '男',
            age: 18
        }

        //渲染组件到页面
        ReactDOM.render(<Person name="tom" sex="女" age={18}/>, document.getElementById("test"));
    </script>
</body>

</html>
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM0NjkzODA3Ml19
-->