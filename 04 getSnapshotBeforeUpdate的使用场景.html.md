<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .list {
            width: 200px;
            height: 150px;
            background-color: skyblue;
            overflow: auto;
        }

        .news {
            height: 30px
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
        /*
        react17声明周期(新)
        1. 初始化阶段：由ReactDOM.render()触发——初次渲染
            A. constructor()
            B. getDerivedStateFromProps()
            C. render()
            D. componentDidMount()=====>常用
        2. 更新阶段：由组件内部this.setState()或父组件重新render触发
            A. getDerivedStateFromProps()
            B. shouldComponentUpdate()
            C. render()=====>常用
            D. getSnapshotBeforeUpdate()
            E. componentDidUpdate（）
        3. 卸载组件：由ReactDOM.unmountComponentAtNode()触发
            A. componentWillUnmount()=====>常用
        */
        class NewsList extends React.Component {

            state = {
                newsArr: []
            }

            render() {
                return (
                    <div className="list" ref="list">
                        {
                            this.state.newsArr.map((newsItem,index)=>{
                                return <div key={index} className='news'>{newsItem}</div>
                            })
                        }
                    </div>
                )
            }

            getSnapshotBeforeUpdate(){
                return this.refs.list.scrollHeight
            }

            componentDidUpdate(preProps,preState,height){
                this.refs.list.scrollTop+=this.refs.list.scrollHeight-height;
            }

            componentDidMount() {
                setInterval(() => {
                    //获取原装态
                    const { newsArr } = this.state
                    //模拟一条新闻
                    const news = '新闻'+(newsArr.length+1)
                    //更新状态
                    this.setState({
                        newsArr:[news,...newsArr]
                    })
                }, 1000)
            }
        }

        ReactDOM.render(<NewsList />, document.getElementById('test'));
    </script>
</body>

</html>
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU3MDcxOTcwNF19
-->