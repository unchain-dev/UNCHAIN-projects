### ð ã¹ãã¼ãã³ã³ãã©ã¯ããä½æãã

ã³ã¼ãã£ã³ã°ã®åã«ä»åä½æãã to-do ã¢ããªã«å¿è¦ã¨ãªãæ©è½ãæ´çãã¦ããã¾ãããã

1. to-do ãä½æããæ©è½

2. to-do ãæ´æ°ããæ©è½

3. to-do ã®å®äºã»æªå®äºãåãæ¿ããæ©è½

4. to-do ãåé¤ããæ©è½

ããã§ã¯ãä»¥ä¸ã®ï¼ç¹ãæè­ããªãããã³ã¼ãã£ã³ã°ã«é²ã¿ã¾ãããã

`contracts` ãã©ã«ãã®ä¸­ã« `TodoContract.sol` ãã¡ã¤ã«ãä½æãã¦ãã ããã

`TodoContract.sol` ã®ãã¡ã¤ã«åã«ä»¥ä¸ã®ã³ã¼ããè¨è¼ãã¾ãã

```js
// TodoContract.sol
// SPDX-License-Identifier: GPL-3.0
pragma solidity ^0.8.9;

contract TodoContract {
    uint256 public taskCount = 0;

    struct Task {
        uint256 index;
        string taskName;
        bool isComplete;
    }

    mapping(uint256 => Task) public todos;
    //1.to-doãä½æããæ©è½
    event TaskCreated(string task, uint256 taskNumber);
    //2.to-doãæ´æ°ããæ©è½
    event TaskUpdated(string task, uint256 taskId);
    //3.to-doã®å®äºã»æªå®äºãåãæ¿ããæ©è½
    event TaskIsCompleteToggled(string task, uint256 taskId, bool isComplete);
    //4.to-doãåé¤ããæ©è½
    event TaskDeleted(uint256 taskNumber);
}

```

ã§ã¯ãã³ã¼ããè©³ããè¦ã¦ããã¾ãããã

```js
// TodoContract.sol
// SPDX-License-Identifier: GPL-3.0
```

ããã¯ãSPDX ã©ã¤ã»ã³ã¹è­å¥å­ãã¨å¼ã°ãã¾ãã

è©³ç´°ã«ã¤ãã¦ã¯ã[ãã¡ã](https://www.skyarch.net/blog/?p=15940)ãåç§ãã¦ã¿ã¦ãã ããã

```js
// TodoContract.sol
pragma solidity ^0.8.9;
```

ããã¯ãã³ã³ãã©ã¯ãã§ä½¿ç¨ãã Solidity ã³ã³ãã¤ã©ã®ãã¼ã¸ã§ã³ã§ãã

ä¸è¨ã®å ´åããã®ã³ã³ãã©ã¯ããå®è¡ããã¨ãã¯ãSolidity ã³ã³ãã¤ã©ã®ãã¼ã¸ã§ã³ 0.8.6 ã®ã¿ãä½¿ç¨ããããä»¥ä¸ã®ãã®ã¯ä½¿ç¨ãã¾ãããã¨ããæå³ã§ãã

```js
// TodoContract.sol
contract TodoContract {
  ...
}
```

`contract` ã¯ãã»ãã®è¨èªã§ããã¨ããã®ã[class](https://wa3.i-3-i.info/word1120.html)ãã®ãããªãã®ãªã®ã§ãã

```js
// TodoContract.sol
    uint256 public taskCount = 0;
```

`taskCount` ã¯ãã¹ãã¼ãã³ã³ãã©ã¯ãåã®ToDoã¢ã¤ãã ã®ç·æ°ãæ ¼ç´ããç¬¦å·ãªãpublicæ´æ°ã§ãã

```js
// TodoContract.sol
    struct Task {
        uint256 index;
        string taskName;
        bool isComplete;
    }
```

`struct Task` ã¯ãåToDoã«é¢ããæå ±ï¼ã¡ã¿ãã¼ã¿ï¼ãæ ¼ç´ããããã®ãã¼ã¿æ§é ã§ããããã«ã¯ãTo-doã® `id`ã`taskName`ã`isComplete` ã®ãã¼ã«å¤ãªã©ãå«ã¾ãã¦ãã¾ãã
- `id` : To-doãè­å¥ããããã®id
- `taskName` : To-doã®ã¿ã¤ãã«
- `isComplete` : To-doãå®äºãããã©ããã®ç¶æï¼å®äºããã`true`ãå®äºãã¦ãªããªã `false` ï¼

```js
// TodoContract.sol
    mapping(uint256 => Task) public todos;
```

`mapping(uint256 => Task) public todos;` ã¯ããã¹ã¦ã®ToDoãæ ¼ç´ãããããã³ã°ã§ãã­ã¼ã¯ `id` ã§ãå¤ã¯ä¸è¨ã® `Task` ã§ãã

```js
// TodoContract.sol
    //1.to-doãä½æããæ©è½
    event TaskCreated(string task, uint256 taskNumber);
    //2.to-doãæ´æ°ããæ©è½
    event TaskUpdated(string task, uint256 taskId);
    //3.to-doã®å®äºã»æªå®äºãåãæ¿ããæ©è½
    event TaskIsCompleteToggled(string task, uint256 taskId, bool isComplete);
    //4.to-doãåé¤ããæ©è½
    event TaskDeleted(uint256 taskNumber);
```
`TaskCreated`ã`TaskUpdated`ã`TaskIsCompleteToggled`ã`TaskDeleted` ã¯ããã­ãã¯ãã§ã¼ã³ä¸ã§çºçããã¤ãã³ãã§ãdAppã¯ããããªã¹ãã³ã°ããããã«å¿ãã¦æ©è½ãããã¨ãã§ãã¾ãã



æ¬¡ã«ä»¥ä¸ã®ã³ã¼ãã `TodoContract` åã® `event TaskDeleted(uint256 taskNumber);` ä¸ã«è¿½å ãã¦ãã ããã

1\. to-do ãä½æããæ©è½

```js
// TodoContract.sol
    function createTask(string memory _taskName) public {
        todos[taskCount] = Task(taskCount, _taskName, false);
        taskCount++;
        emit TaskCreated(_taskName, taskCount - 1);
    }
```

ã§ã¯ãã³ã¼ããè©³ããè¦ã¦ããã¾ãããã

```js
// TodoContract.sol
    function createTask(string memory _taskName) public {
    ã...
    }
```

`createTask`é¢æ°ã¯ãto-doã®`_taskName`ãåãåãã¾ãã

```js
// TodoContract.sol
        todos[taskCount] = Task(taskCount, _taskName, false);
```

`taskCount` ã¨ `_taskName` ã§æ°ãã `Task` æ§é ãä½æãã`todos` ãããã®ç¾å¨ã® `taskCount` ã®å¤ã«ä»£å¥ãããã¨ãã§ãã¾ãã

```js
// TodoContract.sol
        taskCount++;
```

to-doãä½æããããã³ã« `taskCount` ãï¼ãã¤å¢ããããã«ãã¦ãã¾ãã

```js
// TodoContract.sol
        emit TaskCreated(_taskName, taskCount - 1);
```

ãã¹ã¦ãå®äºãããã`TaskCreated` ã¤ãã³ãã `emit` ããå¿è¦ãããã¾ãã

æ¬¡ã«ä»¥ä¸ã®ã³ã¼ãã `TodoContract` åã® `createTask` é¢æ°ã®ä¸ã«è¿½å ãã¦ãã ããã

2\.to-doãæ´æ°ããæ©è½

```js
// TodoContract.sol
    function updateTask(uint256 _taskId, string memory _taskName) public {
        Task memory currTask = todos[_taskId];
        todos[_taskId] = Task(_taskId, _taskName, currTask.isComplete);
        emit TaskUpdated(_taskName, _taskId);
    }
```

ã§ã¯ãã³ã¼ããè©³ããè¦ã¦ããã¾ãããã

```js
// TodoContract.sol
    function updateTask(uint256 _taskId, string memory _taskName) public {
      ...
    }
```

`updateTask` é¢æ°ã¯ãæ´æ°ãããto-doã® `_taskId` ã¨æ´æ°ããã `taskName` ãåãåãã¾ãã

```js
// TodoContract.sol
        Task memory currTask = todos[_taskId];
        todos[_taskId] = Task(_taskId, _taskName, currTask.isComplete);
```

- ãããã®å¤ã§æ°ãã `Task` æ§é ãä½æããåãåã£ã `_taskId` ã«å¯¾å¿ãã `todos` ãããã«å²ãå½ã¦ããã¨ãã§ãã¾ãã

- æ´æ°ä¸­ã«ããã®to-doã® `isComplete` ã®å¤ãä¿æãã¦ããå¿è¦ãããã¾ããã¾ãããããããç¾å¨ã®ã¿ã¹ã¯ãåå¾ãããããå¤æ°ã«æ ¼ç´ãããã® `isComplete` å¤ãæ°ããã¿ã¹ã¯ã»ãªãã¸ã§ã¯ãã«ä½¿ç¨ãã¾ãã

```js
// TodoContract.sol
        emit TaskUpdated(_taskName, _taskId);
```

ãã¹ã¦ãå®äºãããã`TaskUpdated` ã¤ãã³ãã `emit` ããå¿è¦ãããã¾ãã

æ¬¡ã«ä»¥ä¸ã®ã³ã¼ãã `TodoContract` åã® `updateTask` é¢æ°ã®ä¸ã«è¿½å ãã¦ãã ããã

3\.to-doã®å®äºã»æªå®äºãåãæ¿ããæ©è½

```js
// TodoContract.sol
    function toggleComplete(uint256 _taskId) public {
        Task memory currTask = todos[_taskId];
        todos[_taskId] = Task(_taskId, currTask.taskName, !currTask.isComplete);

        emit TaskIsCompleteToggled(
            currTask.taskName,
            _taskId,
            !currTask.isComplete
        );
    }
```

ã§ã¯ãã³ã¼ããè©³ããè¦ã¦ããã¾ãããã

```js
// TodoContract.sol
    function toggleComplete(uint256 _taskId) public {
      ...
    }
```

`toggleComplete` é¢æ°ã«ã¯ãæ´æ°ããto-doã® `_taskId` ãåãåãã¾ãã

```js
// TodoContract.sol
        Task memory currTask = todos[_taskId];
        todos[_taskId] = Task(_taskId, currTask.taskName, !currTask.isComplete);
```
- `todos` ããããã `Task` ãªãã¸ã§ã¯ããåå¾ãããã®å¤ã§æ°ãã `Task` ãªãã¸ã§ã¯ããä½æãã¾ãã

- `isComplete` ãç¾å¨ã® `isComplete` ã®åå¯¾ã®å¤ã¨ãã¦è¨­å®ãã¾ãã

```js
// TodoContract.sol
        emit TaskIsCompleteToggled(
            currTask.taskName,
            _taskId,
            !currTask.isComplete
        );
```

ãã¹ã¦ãå®äºãããã`TaskIsCompleteToggled` ã¤ãã³ãã `emit` ããå¿è¦ãããã¾ãã

æå¾ã«ä»¥ä¸ã®ã³ã¼ãã `TodoContract` åã® `toggleComplete` é¢æ°ã®ä¸ã«è¿½å ãã¦ãã ããã

4\.to-doãåé¤ããæ©è½

```js
// TodoContract.sol
    function deleteTask(uint256 _taskId) public {
        delete todos[_taskId];
        emit TaskDeleted(_taskId);
    }
```

ã§ã¯ãã³ã¼ããè©³ããè¦ã¦ããã¾ãããã

```js
// TodoContract.sol
    function deleteTask(uint256 _taskId) public {
  ...
    }
```

`deleteTask` ã¯ãåé¤ããto-doã® `_task` ããã©ã¡ã¼ã¿ã¨ãã¦åãåãã¾ãã

```js
// TodoContract.sol
        delete todos[_taskId];
```

åãåã£ã `_task` ã«å¯¾å¿ãã `todos` ããããã `Task` ãªãã¸ã§ã¯ããåé¤ãã¾ãã

```js
// TodoContract.sol
        emit TaskDeleted(_taskId);
```

ãã¹ã¦ãå®äºãããã`TaskDeleted` ã¤ãã³ãã `emit` ããå¿è¦ãããã¾ãã

ã¹ãã¼ãã³ã³ãã©ã¯ãã®éçºã¯ä»¥ä¸ã§å®äºã§ãããã¨ã¯ãã³ã³ãã¤ã«ã¨ããã­ã¤ã®ä½æ¥­ãé²ããã ãã§ãã
### ðââï¸ è³ªåãã

ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscord ã® `#section-1` ã§è³ªåããã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã® 3 ç¹ãè¨è¼ãã¦ãã ãã â¨

```
1. è³ªåãé¢é£ãã¦ããã»ã¯ã·ã§ã³çªå·ã¨ã¬ãã¹ã³çªå·
2. ä½ããããã¨ãã¦ããã
3. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
4. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```

---

æ¬¡ã®ã¬ãã¹ã³ã«é²ãã§ãã¹ãã¼ãã³ã³ãã©ã¯ãã®ã³ã³ãã¤ã«ã¨ããã­ã¤ã®ä½æ¥­ãéå§ãã¾ããã ð
