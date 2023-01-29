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
        //创建组件
        class Person extends React.Component {
            //1. 构造器接住了参数props，如果传给super和不传给super有什么区别？
            //2. 类中的构造器有什么作用？
            //3. 构造器一般可以省略，如果不省略，构造器里可以做什么事情？

            //构造器是否接收props，是否传递给super，取决于是否希望在构造器中，通过(实例)this访问props
            //类中的构造器，能省略，则省略
            constructor(props){//接props
                //console.log(props);
                super(props);//传props
                console.log('constructor: ',this.props)//如果不接不传，这里显示undefined
            }

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

        //渲染组件到页面
        ReactDOM.render(<Person name="tom" />, document.getElementById("test"));
    </script>
</body>

</html>
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2ODk1MTY0NDZdfQ==
-->