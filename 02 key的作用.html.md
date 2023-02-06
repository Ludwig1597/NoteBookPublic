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
        经典面试题：
        1. react/vue中的key有什么作用？（key的内部原理是什么？）
        2. 为什么遍历列表时，key最好不要用index

        A. 虚拟DOM中key的作用：
            a. 简单的说：key是虚拟DOM对象的标识，在更新显示时key起着极其重要的作用
            b. 详细的说：当状态中的数据发生变化时，react会根据【新数据】生成【新的虚拟DOM】
                        随后React进行【新虚拟DOM】与【旧虚拟DOM】的diff比较，比较规则如下：
                        - 旧虚拟DOM中找到了与新虚拟DOM相同的key：
                            - 若虚拟DOM中内容没变，直接使用之前的真实DOM
                            - 若虚拟DOM中内容改变，则生成新的真实DOM，随后替换掉页面中之前的真实DOM
                        - 旧虚拟DOM中未找到与新虚拟DOM相同的key：
                            - 根据数据创建新的真实DOM，随后渲染到页面
        B. 用index作为key可能会引发的问题：
            a. 若对数据进行：逆序添加、逆序删除等破坏顺序操作：
                - 会产生没有必要的真实DOM更新 ==> 界面效果没问题，但效率低
            b. 如果结构中还包含输入类的DOM：
                - 会产生错误的DOM更新 ==> 界面有问题
            c. 注意！如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示数据，使用index作为key是没有问题的
        C. 开发中，如何选择key？
            a. 最好使用每条数据的唯一标识作为key，比如id、手机号、身份证号、学号等唯一值
            b. 如果确定只是简单的展示数据，用index也是可以的
        */

        /*
        慢动作回放————使用index索引值作为key
        初始数据：
            {id:1,name:'小张',age:18},
            {id:2,name:'小李',age:20} 
        初始的虚拟DOM：
            <li key=0>小张---18 <input type="text"/> </li>
            <li key=1>小李---20 <input type="text"/> </li>
        更新后的数据：
            {id:3,name:'小王',age:32},
            {id:1,name:'小张',age:18},
            {id:2,name:'小李',age:20} 
        更新数据后的虚拟DOM：
            <li key=0>小王---32 <input type="text"/> </li>
            <li key=1>小张---18 <input type="text"/> </li>
            <li key=2>小李---20 <input type="text"/> </li>
        ==============================================
        慢动作回放————使用id唯一标识作为key
        初始数据：
            {id:1,name:'小张',age:18},
            {id:2,name:'小李',age:20} 
        初始的虚拟DOM：
            <li key=1>小张---18 <input type="text"/> </li>
            <li key=2>小李---20 <input type="text"/> </li>
        更新后的数据：
            {id:3,name:'小王',age:32},
            {id:1,name:'小张',age:18},
            {id:2,name:'小李',age:20} 
        更新数据后的虚拟DOM：
            <li key=3>小王---32 <input type="text"/> </li>
            <li key=1>小张---18 <input type="text"/> </li>
            <li key=2>小李---20 <input type="text"/> </li>

        */
        class Person extends React.Component{
            state={
                people:[
                   {id:1,name:'小张',age:18},
                   {id:2,name:'小李',age:20} 
                ]
            }

            add=()=>{
                const {people}=this.state
                const p={
                    id:people.length+1,
                    name: '小王',
                    age: 32
                }
                this.setState({
                    people:[p,...people]
                })
            }

            render(){
                return (
                    <div>
                        <h2>展示人员信息</h2>
                        <button onClick={this.add}>添加一个小王</button>
                        <h3>使用index(索引值)作为key</h3>
                        <ul>
                            {
                                this.state.people.map((personObj,index)=>{
                                    return <li key={index}>{personObj.name}---{personObj.age} <input type="text"/> </li>
                                })
                            }
                        </ul>
                        <hr />
                        <h3>使用id(数据的唯一标识)作为key</h3>
                        <ul>
                            {
                                this.state.people.map((personObj)=>{
                                    return <li key={personObj.id}>{personObj.name}---{personObj.age} <input type="text"/></li>
                                })
                            }
                        </ul>
                    </div>
                )
            }
        }
        ReactDOM.render(<Person />,document.getElementById('test'));
    </script>
</body>

</html>
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc2NTM2ODQyNV19
-->