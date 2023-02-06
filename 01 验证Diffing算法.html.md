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
   //13 DOM的diffing算法
   // 01 验证Diffing算法
    <div id="test"></div>
    <script type="text/javascript" src="./../99 react17/react.development.js"></script>
    <script type="text/javascript" src="./../99 react17/react-dom.development.js"></script>
    <script type="text/javascript" src="./../99 react17/babel.min.js"></script>
    <script type="text/javascript" src="./../99 react17/prop-types.js"></script>

    <script type="text/babel">
        class Time extends React.Component{
            state={
                date: new Date()
            }

            render(){
                return (
                    <div>
                        <h1>hello</h1>
                        <input type='text' />
                        <span>现在是：{this.state.date.toTimeString()}</span>
                    </div>
                )
            }

            componentDidMount(){
                setInterval(()=>{
                    this.setState({
                        date: new Date()
                    })
                },1000)
            }
        }
        ReactDOM.render(<Time />,document.getElementById('test'));
    </script>
</body>

</html>
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjUyNzY2Mzc2XX0=
-->