```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React App</title>
    <link rel="stylesheet" href="index.css">
</head>
<body>
    <div id="root">
        <div class="todo-container">
            <div class="todo-wrap">
                <div class="todo-header">
                    <input type="text" placeholder="请输入任务名称，按回车键确认" />
                </div>
                <ul class="todo-main">
                    <li>
                        <label>
                            <input type="checkbox" />
                            <span>xxxxx</span>
                        </label>
                        <button class="btn btn-danger" style="display:none">删除</button>
                    </li>
                    <li>
                        <label>
                            <input type="checkbox" />
                            <span>yyyyy</span>
                        </label>
                        <button class="btn btn-danger" style="display:none">删除</button>
                    </li>
                </ul>
                <div class="todo-footer">
                    <label>
                        <input type="checkbox">
                    </label>
                    <span>
                        <span>已完成0</span> / 全部2
                    </span>
                    <button class="btn btn-danger">清除已完成任务</button>
                </div>
            </div>
        </div>
    </div>
</body>
</html>
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQ0Njk2MTMzMV19
-->