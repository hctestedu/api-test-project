## 纯接口项目-完整接口文档

> 数据库和接口服务部署运行在你自己的电脑上面
>
> ！！任何时候都可以实战
>
> ！！ 接口自动化测试 结合 数据库校验

## 不会编译运行安装环境？

> 项目涉及数据库和JAVA项目的编译，不会操作单独联系我

[点我免费获取可运行版本](https://wtnjm.xet.tech/s/4fmrTx)

[点我免费获取可运行版本](https://wtnjm.xet.tech/s/4fmrTx)

[点我免费获取可运行版本](https://wtnjm.xet.tech/s/4fmrTx)



## 考试系统功能说明及接口文档

### 学生系统功能

| 模块     | 介绍                                                     |
| -------- | -------------------------------------------------------- |
| 登录     | 用户名、密码                                             |
| 注册     | 年级、用户名、密码                                       |
| 任务中心 | 管理员发布的年级任务，每个学生只能做一次                 |
| 考试     | 题干支持文本、图片、数学公式、表格等，学生答题支持：文本 |
| 固定试卷 | 可重复练习、自行批改的试卷                               |
| 时段试卷 | 在时间限制内，可重复练习、自行批改的试卷                 |
| 考试记录 | 查看答卷记录和试卷信息                                   |
| 错题本   | 答错题目会自动进入错题本，显示题目基本信息               |
| 个人信息 | 显示学生个人资料                                         |
| 更新信息 | 修改个人资料、头像                                       |
| 个人动态 | 显示用户最近的个人动态                                   |
| 消息中心 | 用于接收管理员发送的消息                                 |

### 1.2 管理系统功能

| 模块       | 介绍                                                         |
| ---------- | ------------------------------------------------------------ |
| 登录       | 用户名、密码                                                 |
| 主页       | 试卷总数、题目总数、用户活跃度、题目月数量                   |
| 学生列表   | 显示系统所有的学生，新增、修改、删除、禁用                   |
| 管理员列表 | 显示系统所有的管理员，新增、修改、删除、禁用                 |
| 学科列表   | 学科查询、修改、删除                                         |
| 学科创编   | 创建学科                                                     |
| 试卷列表   | 试卷查询、修改、删除                                         |
| 试卷创编   | 创建的试卷为时段试卷、固定试卷、任务试卷                     |
| 题目列表   | 题目查询、修改、删除                                         |
| 题目创建   | 题目支持单选题、多选题、判断题、填空题、简答题，题干支持文本、图片、表格、数学公式 |
| 任务列表   | 任务查询、修改、删除                                         |
| 消息列表   | 显示已发送的消息，消息已读人数等信息                         |
| 消息发送   | 发送消息给多个用户                                           |
| 用户日志   | 显示所有用户日志                                             |
| 个人资料   | 显示管理员用户名、真实姓名                                   |
| 时间线     | 显示管理员创建时间                                           |
| 修改资料   | 修改姓名、手机号                                             |

# 数据库设计

### 3.1 试卷表

- 表名：t_exam_paper
- 字段注释：

| 字段名                | 类型     | 注释                                         |
| --------------------- | -------- | -------------------------------------------- |
| id                    | int      |                                              |
| name                  | varchar  | 试卷名称                                     |
| subject_id            | int      | 学科                                         |
| paper_type            | int      | 试卷类型( 1.固定试卷 4.时段试卷 6.任务试卷 ) |
| grade_level           | int      | 年级                                         |
| score                 | int      | 试卷总分(千分制)                             |
| question_count        | int      | 题目数量                                     |
| suggest_time          | int      | 建议时长(分钟)                               |
| limit_start_time      | datetime | 时段试卷 开始时间                            |
| limit_end_time        | datetime | 时段试卷 结束时间                            |
| frame_text_content_id | int      | 试卷框架 内容为JSON                          |
| create_user           | int      |                                              |
| create_time           | datetime |                                              |
| deleted               | bit      |                                              |
| task_exam_id          | int      |                                              |

### 3.2 试卷答案表

- 表名：t_exam_paper_answer
- 字段注释：

| 字段名           | 类型     | 注释                                         |
| ---------------- | -------- | -------------------------------------------- |
| id               | int      |                                              |
| exam_paper_id    | int      |                                              |
| paper_name       | varchar  | 试卷名称                                     |
| paper_type       | int      | 试卷类型( 1.固定试卷 4.时段试卷 6.任务试卷 ) |
| subject_id       | int      | 学科                                         |
| system_score     | int      | 系统判定得分                                 |
| user_score       | int      | 最终得分(千分制)                             |
| paper_score      | int      | 试卷总分                                     |
| question_correct | int      | 做对题目数量                                 |
| question_count   | int      | 题目总数量                                   |
| do_time          | int      | 做题时间(秒)                                 |
| status           | int      | 试卷状态(1待判分 2完成)                      |
| create_user      | int      | 学生                                         |
| create_time      | datetime | 提交时间                                     |
| task_exam_id     | int      |                                              |

### 3.3 试卷题目答案表

- 表名：t_exam_paper_question_customer_answer
- 字段注释：

| 字段名                   | 类型     | 注释         |
| ------------------------ | -------- | ------------ |
| id                       | int      |              |
| question_id              | int      | 题目Id       |
| exam_paper_id            | int      | 答案Id       |
| exam_paper_answer_id     | int      |              |
| question_type            | int      | 题型         |
| subject_id               | int      | 学科         |
| customer_score           | int      | 得分         |
| question_score           | int      | 题目原始分数 |
| question_text_content_id | int      | 问题内容     |
| answer                   | varchar  | 做题答案     |
| text_content_id          | int      | 做题内容     |
| do_right                 | bit      | 是否正确     |
| create_user              | int      | 做题人       |
| create_time              | datetime |              |
| item_order               | int      |              |

### 3.4 消息表

- 表名：t_message
- 字段注释：

| 字段名             | 类型     | 注释           |
| ------------------ | -------- | -------------- |
| id                 | int      |                |
| title              | varchar  | 标题           |
| content            | varchar  | 内容           |
| create_time        | datetime |                |
| send_user_id       | int      | 发送者用户ID   |
| send_user_name     | varchar  | 发送者用户名   |
| send_real_name     | varchar  | 发送者真实姓名 |
| receive_user_count | int      | 接收人数       |
| read_count         | int      | 已读人数       |

### 3.5 用户消息表

- 表名：t_message_user
- 字段注释：

| 字段名            | 类型     | 注释           |
| ----------------- | -------- | -------------- |
| id                | int      |                |
| message_id        | int      | 消息内容ID     |
| receive_user_id   | int      | 接收人ID       |
| receive_user_name | varchar  | 接收人用户名   |
| receive_real_name | varchar  | 接收人真实姓名 |
| readed            | bit      | 是否已读       |
| create_time       | datetime |                |
| read_time         | datetime | 阅读时间       |

### 3.6 题目表

- 表名：t_question
- 字段注释：

| 字段名               | 类型     | 注释                                         |
| -------------------- | -------- | -------------------------------------------- |
| id                   | int      |                                              |
| question_type        | int      | 1.单选题 2.多选题 3.判断题 4.填空题 5.简答题 |
| subject_id           | int      | 学科                                         |
| score                | int      | 题目总分(千分制)                             |
| grade_level          | int      | 级别                                         |
| difficult            | int      | 题目难度                                     |
| correct              | text     | 正确答案                                     |
| info_text_content_id | int      | 题目 填空、 题干、解析、答案等信息           |
| create_user          | int      | 创建人                                       |
| status               | int      | 1.正常                                       |
| create_time          | datetime | 创建时间                                     |
| deleted              | bit      |                                              |

### 3.7 学科表

- 表名：t_subject
- 字段注释：

| 字段名     | 类型    | 注释                            |
| ---------- | ------- | ------------------------------- |
| id         | int     |                                 |
| name       | varchar | 语文 数学 英语 等               |
| level      | int     | 年级 (1-12) 小学 初中 高中 大学 |
| level_name | varchar | 一年级、二年级等                |
| item_order | int     | 排序                            |
| deleted    | bit     |                                 |

### 3.8 任务表

- 表名：t_task_exam
- 字段注释：

| 字段名                | 类型     | 注释                |
| --------------------- | -------- | ------------------- |
| id                    | int      |                     |
| title                 | varchar  |                     |
| grade_level           | int      | 级别                |
| frame_text_content_id | int      | 任务框架 内容为JSON |
| create_user           | int      |                     |
| create_time           | datetime |                     |
| deleted               | bit      |                     |
| create_user_name      | varchar  |                     |

### 3.9 用户任务表

- 表名：t_task_exam_customer_answer
- 字段注释：

| 字段名          | 类型     | 注释               |
| --------------- | -------- | ------------------ |
| id              | int      |                    |
| task_exam_id    | int      |                    |
| create_user     | int      |                    |
| create_time     | datetime |                    |
| text_content_id | int      | 任务完成情况(Json) |

### 3.10 文本表

- 表名：t_text_content
- 字段注释：

| 字段名      | 类型     | 注释 |
| ----------- | -------- | ---- |
| id          | int      |      |
| content     | text     |      |
| create_time | datetime |      |

### 3.11 用户表

- 表名：t_user
- 字段注释：

| 字段名           | 类型     | 注释            |
| ---------------- | -------- | --------------- |
| id               | int      |                 |
| user_uuid        | varchar  |                 |
| user_name        | varchar  | 用户名          |
| password         | varchar  |                 |
| real_name        | varchar  | 真实姓名        |
| age              | int      |                 |
| sex              | int      | 1.男 2女        |
| birth_day        | datetime |                 |
| user_level       | int      | 学生年级(1-12)  |
| phone            | varchar  |                 |
| role             | int      | 1.学生 3.管理员 |
| status           | int      | 1.启用 2禁用    |
| image_path       | varchar  | 头像地址        |
| create_time      | datetime |                 |
| modify_time      | datetime |                 |
| last_active_time | datetime |                 |
| deleted          | bit      | 是否删除        |
| wx_open_id       | varchar  | 微信openId      |

### 3.12 用户日志表

- 表名：t_user_event_log
- 字段注释：

| 字段名      | 类型     | 注释     |
| ----------- | -------- | -------- |
| id          | int      |          |
| user_id     | int      | 用户id   |
| user_name   | varchar  | 用户名   |
| real_name   | varchar  | 真实姓名 |
| content     | text     | 内容     |
| create_time | datetime | 时间     |

### 3.13 用户Token表

- 表名：t_user_token
- 字段注释：

| 字段名      | 类型     | 注释       |
| ----------- | -------- | ---------- |
| id          | int      |            |
| token       | varchar  |            |
| user_id     | int      | 用户Id     |
| wx_open_id  | varchar  | 微信openId |
| create_time | datetime |            |
| end_time    | datetime |            |
| user_name   | varchar  | 用户名     |

# 学生端

### 4.1.1 登录

- 接口地址：/api/user/login
- 请求参数：

```text
{
    "userName": "student",  //用户名
    "password": "",  //密码
    "remember": false  //下次自动登录
}
```

- 返回参数：

```text
{
        "userName": "student",  //用户名
        "imagePath": "",  //头像
}
```

### 4.1.2 注册

- 接口地址：/api/student/user/register
- 请求参数：

```text
{
    "userName": "student5", //用户名
    "password": "123456",  //密码
    "userLevel": 1  //年级
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": null
}
```

### 4.1.3 登出

- 接口地址：/api/user/logout
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": null
}
```

### 4.1.4 首页

- 接口地址：/api/student/dashboard/index
- 请求参数：无
- 返回参数：

```text
{
    "fixedPaper": [  //固定试卷
        {
            "id": 2399,  //试卷Id
            "name": "test33333",  //试卷名称
            "limitStartTime": null,  //考试开始时间
            "limitEndTime": null     //考试结束时间
        }
    ],
    "timeLimitPaper": []    //时段试卷
}
```

### 4.1.5 任务中心

- 接口地址：/api/student/dashboard/task
- 请求参数：无
- 返回参数：

```text
[
        {
            "id": 14,  //任务id
            "title": "2021-04-25作业",  //任务标题
            "paperItems": [
                {
                    "examPaperId": 181,   //任务试卷id
                    "examPaperName": "第一次出卷",  //任务试卷名称
                    "examPaperAnswerId": 579,  //答卷id
                    "status": 2  //答卷状态
                }
            ]
        }
    ]
```

### 4.1.6 学科列表

- 接口地址：/api/student/education/subject/list
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": [
        {
            "id": "18",  //学科id
            "name": "英语"  //学科名称
        }
    ]
}
```

### 4.1.7 试卷分页

- 接口地址：/api/student/exam/paper/pageList
- 请求参数：

```text
{
    "paperType": 1, //试卷类型
    "subjectId": 158, //学科id
    "pageIndex": 1, //页数
    "pageSize": 10  //每页条数
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "total": 1,
        "list": [
            {
                "id": 2520,  //试卷id
                "name": "生理卫生",  //试卷名称
                "questionCount": 1,  //题目数
                "score": 20,  //试卷分数
                "createTime": "2021-05-31 13:34:49", //创建时间
                "createUser": 2,   //创建人
                "subjectId": 158,  //学科
                "subjectName": "英语",  //学科
                "paperType": 1,   //试卷类型
                "frameTextContentId": 9016  //试卷内容
            }
        ]
    }
}
```

### 4.1.8 试卷查询

- 接口地址：/api/student/exam/paper/select/9
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "id": 14,  //试卷id
        "level": 1,  //年级
        "subjectId": 1,  //学科
        "paperType": 1,  //试卷类型
        "name": "测试一",  //试卷名称
        "suggestTime": 22,  //建议时长
        "limitDateTime": null,  //考试时间限制
        "titleItems": [  
            {
                "name": "一、选择题",  //试卷标题
                "questionItems": [
                    {
                        "id": 14,      //题目id
                        "questionType": 5,  //题型
                        "subjectId": 1,  //学科
                        "title": "默写咏鹅",  //标题
                        "gradeLevel": 1,  //年级
                        "items": [],  //选项
                        "analyze": "咏鹅可以带拼音",  //解析
                        "correctArray": null,  //标答
                        "correct": "鹅鹅鹅， 曲项向天歌。 白毛浮绿水， 红掌拨清波。",  //标答
                        "score": "10", //分数
                        "difficult": 3,  //难度
                        "itemOrder": 1  //顺序
                    }
                ]
            }
        ],
        "score": "10"
    }
}
```

### 4.1.9 试卷提交

- 接口地址：/api/student/exampaper/answer/answerSubmit
- 请求参数：

```text
{
    "questionId": null, 
    "doTime": 14,    //耗时
    "answerItems": [
        {
            "questionId": 4,  //题目id
            "content": null,  //答题内容
            "contentArray": [   //填空题内容
                "测试",
                "1"
            ],
            "completed": true, //是否完成
            "itemOrder": 1   //题目序号
        } 
    ],
    "id": 4   //试卷id
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": "2"   //试卷得分
}
```

### 4.1.10 答卷查询

- 接口地址：/api/student/exampaper/answer/read/4
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "paper": {  //试卷信息
            "id": 14,  //试卷id
            "level": 1, //年级
            "subjectId": 1,  //学科
            "paperType": 4,  //试卷类型
            "name": "限时考试二",  //试卷名称
            "suggestTime": 20,  //考试时长
            "limitDateTime": [  //考试时间限制
                "2021-06-22 00:00:00",
                "2021-08-06 00:00:00"
            ],
            "titleItems": [
                {
                    "name": "一、完成题目",  //标题
                    "questionItems": [   //题目列表
                        {
                            "id": 14,  //题目id
                            "questionType": 4,   //题目类型
                            "subjectId": 1,  //学科
                            "title": "曲项向天歌红掌拨清波",  //题目标题
                            "gradeLevel": 1,  //年级
                            "items": [   //题目选项
                                {
                                    "prefix": "1",   //选项标识
                                    "content": "鹅鹅鹅",   //选项内容
                                    "score": "2"  //选项分数
                                },
                                {
                                    "prefix": "2",
                                    "content": "白毛浮绿水",
                                    "score": "2"
                                }
                            ],
                            "analyze": "咏鹅",  //解析
                            "correctArray": [  //标答
                                "鹅鹅鹅",
                                "白毛浮绿水"
                            ],
                            "correct": "",  //标答
                            "score": "4",  //题目分数
                            "difficult": 4, //题目难度
                            "itemOrder": 1 //题目顺序
                        }
                    ]
                }
            ],
            "score": "18"   //试卷分数
        },
        "answer": {  //答卷信息
            "id": 14,  //答卷id
            "doTime": 14,  //耗时
            "score": "2",  //得分
            "answerItems": [   //答题信息
                {
                    "id": 14,  //答题id
                    "questionId": 4,  //题目id
                    "doRight": null,  //是否正确
                    "content": null, //答题内容
                    "itemOrder": 1, //题序
                    "contentArray": [  //答题内容
                        "测试",
                        "1"
                    ],
                    "score": "0", //得分
                    "questionScore": "4"  //题目分数
                }
            ]
        }
    }
}
```

### 4.1.11 试卷批改

- 接口地址：/api/student/exampaper/answer/edit
- 请求参数：

```text
{
    "id": 14,  //答卷id
    "doTime": 14,  //耗时
    "score": "2",  //得分数
    "answerItems": [
        {
            "id": 14, //答题id
            "questionId": 4, //题目id
            "doRight": null,  //是否正确
            "content": null,  //答题内容
            "itemOrder": 1,  //题目顺序
            "contentArray": [  //答题内容
                "测试",
                "1"
            ],
            "score": "4",  //得分
            "questionScore": "4"  //题目分数
        }
    ]
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": "16"  //试卷得分
}
```

### 4.1.12 考试记录分页

- 接口地址：/api/student/exampaper/answer/pageList
- 请求参数：

```text
{
    "pageIndex": 1, //页码
    "pageSize": 10  //每页条数
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "total": 6204,
        "list": [
            {
                "id": 6534,  //试卷id
                "createTime": "2021-06-01 17:56:38",  //创建时间
                "userScore": "0",  //考试分数
                "subjectName": "数学",  //考试学科
                "subjectId": 129, //学科id
                "questionCount": 1,  //题目数量
                "questionCorrect": 0,  //题目正确数
                "paperScore": "3",  //试卷总分
                "doTime": "4 秒",  //耗时
                "paperType": 7,  //试卷类型
                "systemScore": "0",  //系统批改得分
                "status": 2,   //试卷状态
                "paperName": "智能训练试卷 - 1845",  //试卷名称
                "userName": null  //用户名
            }
        ]
    }
}
```

### 4.1.13 错题本分页

- 接口地址：/api/student/question/answer/page
- 请求参数：

```text
{
    "pageIndex": 1, //页码
    "pageSize": 10  //每页条数
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "total": 17002,
        "list": [
            {
                "id": 24928,   //题目id
                "questionType": 1,  //题型
                "createTime": "2021-06-02 16:07:11",  //创建时间
                "subjectName": "语文",  //学科
                "shortTitle": "666"  //题干
            }
        ]
    }
}
```

### 4.1.14 答题详情

- 接口地址：/api/student/question/answer/select/25067
- 请求参数：

```text
{
    "pageIndex": 1, //页码
    "pageSize": 10  //每页条数
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "questionVM": {
            "id": 507,    //题目id
            "questionType": 1,   //题目类型
            "subjectId": 46,  //学科id
            "title": "111",   //题干
            "gradeLevel": 12,    //年级
            "items": [        //选项
                {
                    "prefix": "A",  //选项
                    "content": "A",  //选项内容
                    "score": null    //选项分数
                }
            ],
            "analyze": "D",     //解析
            "correctArray": null,  //标答
            "correct": "D",   //标答
            "score": "2",  //分数
            "difficult": 3,  //难度
            "itemOrder": null  //排序
        },
        "questionAnswerVM": {   //用户答案
            "id": 25067,  
            "questionId": 507,  //题目id
            "doRight": false,   //是否正确
            "content": "A",   //用户答案
            "itemOrder": 2,   //排序
            "contentArray": null,   //用户答案
            "score": "0",  //得分
            "questionScore": "2"  //题目分数
        }
    }
}
```

### 4.1.15 用户动态

- 接口地址：/api/student/user/log
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": [
        {
            "id": 1812,  
            "userId": 1,  //用户id
            "userName": "student",  //用户名
            "realName": "Test",  //用户真实姓名
            "content": "student 登录了学之思开源考试系统",  //动态内容
            "createTime": "2021-06-08 17:12:50"  //创建时间
        }
    ]
}
```

### 4.1.16 当前用户信息

- 接口地址：/api/student/user/current
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "id": 14,
        "userUuid": "d2d29da2-dcb3-4013-b874-727626236f47",
        "userName": "student",  //用户名
        "realName": "Test",  //真实姓名
        "age": 18,   //年龄
        "role": 1,   //角色
        "sex": 1,  //性别
        "birthDay": "2019-09-01 00:00:00",  //生日
        "phone": "158800882",  //手机号
        "lastActiveTime": "",
        "createTime": "2019-09-07 18:55:02",
        "modifyTime": "2021-06-09 17:04:31",
        "status": 1,  //状态
        "userLevel": 1,   //年级
        "classes": "1班",  //用户班级
        "imagePath": ""  //用户头像
    }
}
```

### 4.1.17 修改用户信息

- 接口地址：/api/student/user/update
- 请求参数：

```text
{
    "id": 14,
    "userUuid": "d2d29da2-dcb3-4013-b874-727626236f47",
    "userName": "student",  //用户名
    "realName": "Test",  //真实姓名
    "age": 18,   //年龄
    "role": 1,   //角色
    "sex": 1,  //性别
    "birthDay": "2019-09-01 00:00:00",  //生日
    "phone": "158800882",  //手机号
    "lastActiveTime": "",
    "createTime": "2019-09-07 18:55:02",
    "modifyTime": "2021-06-09 17:04:31",
    "status": 1,  //状态
    "userLevel": 1,   //年级
    "classes": "1班",  //用户班级
    "imagePath": ""  //用户头像
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": null
}
```

### 4.1.18 消息分页

- 接口地址：/api/student/user/message/page
- 请求参数：

```text
{
    "pageIndex": 1, //页码
    "pageSize": 10  //每页条数
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "total": 5,
        "list": [
            {
                "id": 14,
                "title": "rwerw",   //消息标题
                "messageId": 10,
                "content": "sfsdf",  //消息内容
                "readed": true, //是否已读
                "createTime": "2021-06-11 16:32:40",   //创建时间
                "sendUserName": "admin"  //发送人
            }
        ]
    }
}
```

### 4.1.19 消息标记已读

- 接口地址：/api/student/user/message/read/14
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": null
}
```

### [#](https://www.mindskip.net:999/guide/student.html#_4-1-20-未读消息数量)4.1.20 未读消息数量

- 接口地址：/api/student/user/message/unreadCount
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": 0  //未读消息数量
}
```

# 管理端

### 4.3.1 登录

- 接口地址：/api/user/login
- 请求参数：

```text
{
    "userName": "admin",  //用户名
    "password": "",  //密码
    "remember": false  //记住我
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "id": null,
        "userUuid": null,
        "userName": "admin",  //用户名
        "password": null,
        "realName": null,
        "age": null,
        "sex": null,
        "birthDay": null,
        "userLevel": null,
        "phone": null,
        "role": null,
        "status": null,
        "imagePath": null,
        "createTime": null,
        "modifyTime": null,
        "lastActiveTime": null,
        "deleted": null,
        "wxOpenId": null
    }
}
```

### 4.3.2 登出

- 接口地址：/api/user/logout
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": null
}
```

### 4.3.3 首页

- 接口地址：/api/admin/dashboard/index
- 请求参数：无
- 返回参数：

```text
 {
    "examPaperCount": 2413,  //试卷总数
    "questionCount": 1025,  //题目总数
    "doExamPaperCount": 6148,  //总答卷数
    "doQuestionCount": 23945,  //总题数
    "mothDayUserActionValue": [  //活跃度
        85
    ],
    "mothDayDoExamQuestionValue": [  //月做题数
        22
    ],
    "mothDayText": [  //本月天数
        "1"
    ]
}    
```

### 4.3.4 用户分页

- 接口地址：/api/admin/user/page/list
- 请求参数：

```text
{
    "userName": "",  //用户名
    "role": 1,   //角色
    "pageIndex": 1,  //页码
    "pageSize": 10   //每页条数
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "total": 81,  //总数
        "list": [
            {
                "id": 100,     //用户id
                "userUuid": "fd31ab62-c32f-433c-8dc4-c07e653d390a",  //用户uuid
                "userName": "王",  //用户名
                "realName": null,  //真实姓名
                "age": null,  //年龄
                "role": 1,  //角色
                "sex": null,  //性别
                "birthDay": "",  //出生日期          
                "phone": null,   //手机号                 
                "lastActiveTime": "2021-06-21 20:01:26",  //最后活动时间
                "createTime": "2021-06-21 20:01:26",  //创建时间
                "modifyTime": "2021-06-21 20:01:35",  //修改时间
                "status": 1,  //状态
                "userLevel": 1,  //年级
                "imagePath": null   //头像
            }
        ]
    }
}
```

### 4.3.5 用户查询

- 接口地址：/api/admin/user/select/1
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "id": 100,     //用户id
        "userUuid": "fd31ab62-c32f-433c-8dc4-c07e653d390a",  //用户uuid
        "userName": "王",  //用户名
        "realName": null,  //真实姓名
        "age": null,  //年龄
        "role": 1,  //角色
        "sex": null,  //性别
        "birthDay": "",  //出生日期          
        "phone": null,   //手机号                 
        "lastActiveTime": "2021-06-21 20:01:26",  //最后活动时间
        "createTime": "2021-06-21 20:01:26",  //创建时间
        "modifyTime": "2021-06-21 20:01:35",  //修改时间
        "status": 1,  //状态
        "userLevel": 1,  //年级
        "imagePath": null   //头像
    }
}
```

### 4.3.6 用户编辑

- 接口地址：/api/admin/user/edit
- 请求参数：

```text
{
    "id": null,
    "userName": "testzz",  //用户名
    "password": "123456",  //密码
    "realName": "tesx",  //真实姓名
    "role": 1,  //角色
    "status": 1, //状态
    "age": "", //年龄
    "sex": "", //性别
    "birthDay": null, //生日
    "phone": null,  //手机号
    "userLevel": 1  //年级
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "id": 109,
        "userUuid": "321dec89-0656-4736-ae4c-e2b07f4fcc67",  //用户id
        "userName": "testzz", //用户名
        "password": "" //密码
        "realName": "tesx",  //真实姓名
        "age": null, //年龄
        "sex": null, //性别
        "birthDay": null, //生日
        "userLevel": 1, //年级
        "phone": null, //手机号
        "role": 1, //角色
        "status": 1, //状态
        "imagePath": null, //头像
        "createTime": 1624538837259, //创建日期
        "modifyTime": null, //修改时间
        "lastActiveTime": 1624538837259, //最后活动时间
        "deleted": false, //是否删除
        "wxOpenId": null //微信openId
    }
}
```

### 4.3.7 用户删除

- 接口地址：/api/admin/user/delete/3
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,  //返回状态
    "message": "成功", //返回消息
    "response": null
}
```

### 4.3.8 用户状态修改

- 接口地址：/api/admin/user/changeStatus/1
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": 2
}
```

### 4.3.9 学科列表

- 接口地址：/api/admin/education/subject/list
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": [
        {
            "id": 64,  //学科id
            "name": "语文",  //学科名称
            "level": 1,  //年级
            "levelName": "一年级",  //年级名称
            "itemOrder": null,  //排序
            "deleted": false  //是否删除
        }
    ]
}
```

### 4.3.10 学科分页

- 接口地址：/api/admin/education/subject/page
- 请求参数：

```text
{
    "level": null,  //年级
    "pageIndex": 1,
    "pageSize": 10
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "total": 2,
        "list": [
            {
                "id": 64,
                "name": "数学",  //学科名称
                "level": 1,  //年级
                "levelName": "一年级"  //年级名称
            }
        ]
    }
}
```

### 4.3.11 学科查询

- 接口地址：/api/admin/education/subject/select/2
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "id": 64,
        "name": "数学",  //学科名称
        "level": 1,    //年级
        "levelName": "一年级"   //年级名称
    }
}
```

### 4.3.12 学科编辑

- 接口地址：/api/admin/education/subject/edit
- 请求参数：

```text
{
    "id": 64,
    "name": "数学",  //学科名称
    "level": 2,   //年级
    "levelName": "二年级"  //年级名称
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": null
}
```

### 4.3.13 学科删除

- 接口地址：/api/admin/education/subject/delete/3
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": null
}
```

### 4.3.14 试卷分页

- 接口地址：/api/admin/exam/paper/page
- 请求参数：

```text
{
    "id": null,
    "level": null,   //年级
    "subjectId": null,  //学科
    "pageIndex": 1,  //页码
    "pageSize": 10  //每页数量
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "total": 9,
        "list": [
            {
                "id": 64,     //试卷id
                "name": "中级任务二",    //试卷名称
                "questionCount": 5,  //题目总数
                "score": 180, //试卷分数
                "createTime": "2021-01-21 11:49:31",  //创建时间
                "createUser": 2,  //创建人
                "subjectId": 1,  //学科
                "paperType": 6, //试卷类型
                "frameTextContentId": 13  //试卷内容
            }
        ]
    }
}
```

### 4.3.15 试卷查询

- 接口地址：/api/admin/exam/paper/select/9
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "id": 64,   //试卷id
        "level": 1,  //年级
        "subjectId": 1,  //学科
        "paperType": 1,  //试卷类型
        "name": "语文试卷", //试卷名称  
        "suggestTime": 20,  //考试时间
        "limitDateTime": null,  //限时考试
        "titleItems": [
            {
                "name": "一、选择题",  //试卷标题
                "questionItems": [
                    {
                        "id": 64,   //题目id
                        "questionType": 5,  //题目类型
                        "subjectId": 1,  //学科
                        "title": "默写咏鹅", //题干
                        "gradeLevel": 1, //年级
                        "items": [], //题目选项
                        "analyze": "咏鹅可以带拼音",  //解析
                        "correctArray": null,  //标答数组
                        "correct": "鹅鹅鹅， 曲项向天歌。 白毛浮绿水， 红掌拨清波。",  //标答
                        "score": "10",  //题目分数
                        "difficult": 3,  //难度
                        "itemOrder": 1  //题序
                    }
                ]
            }
        ],
        "score": "10"  //试卷总分
    }
}
```

### [#](https://www.mindskip.net:999/guide/admin.html#_4-3-16-试卷编辑)4.3.16 试卷编辑

- 接口地址：/api/admin/exam/paper/edit
- 请求参数：

```text
{
    "id": 64,  //试卷id
    "level": 1,  //年级
    "subjectId": 1,  //学科
    "paperType": 6,  //试卷类型
    "name": "中级任务二",  //试卷名称
    "suggestTime": 20,  //考试时长
    "limitDateTime": null,  //限时
    "titleItems": [
        {
            "name": "一、选择题",  //标题
            "questionItems": [   //题目列表
                {
                    "id": 64,   //题目id
                    "questionType": 2,  //题型
                    "subjectId": 1,  //学科
                    "title": "以下哪些诗句是静夜思的？",  //题干
                    "gradeLevel": 1,  //年级
                    "items": [   //选项
                        {
                            "prefix": "A",   //选项标记
                            "content": "床前明月光",  //选项内容
                            "score": null,  //选项分数
                            "itemUuid": null  //选项标识
                        }
                    ],
                    "analyze": "床前明月光， 疑是地上霜。 举头望明月， 低头思故乡。",  //解析
                    "correctArray": [  //正确答案
                        "A",
                        "C"
                    ],
                    "correct": "A,C", //正确答案
                    "score": "0",  //题目分数
                    "difficult": 3,  //难度
                    "itemOrder": 1  //题序
                }
            ]
        }
    ],
    "score": "18"  //试卷总分
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "id": 64,  //试卷id
        "level": 1,  //年级
        "subjectId": 1,   //学科
        "paperType": 6,   //试卷类型
        "name": "中级任务二",   //试卷名称
        "suggestTime": 20,  //考试时长
        "limitDateTime": null,  //限时
        "titleItems": [
            {
                "name": "一、选择题",  //标题
                "questionItems": [
                    {
                        "id": 64,   //题目id
                        "questionType": 2,    //题型
                        "subjectId": 1,   //学科
                        "title": "以下哪些诗句是静夜思的？",   //题干
                        "gradeLevel": 1,    //年级
                        "items": [   //选项
                            {
                                "prefix": "A",   //选项标记
                                "content": "床前明月光",     //选项内容
                                "score": null,   //选项分数
                                "itemUuid": null  //选项标识
                            }
                        ],
                        "analyze": "床前明月光， 疑是地上霜。 举头望明月， 低头思故乡。",   //解析
                        "correctArray": [   //正确答案
                            "A",
                            "C"
                        ],
                        "correct": "A,C",   //正确答案
                        "score": "0",   //题目分数
                        "difficult": 3,   //难度
                        "itemOrder": 1   //题序
                    }
                ]
            }
        ],
        "score": "18"  //题序
    }
}
```

### 4.3.17 试卷删除

- 接口地址：/api/admin/exam/paper/delete/9
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": null
}
```

### 4.3.18 任务试卷分页

- 接口地址：/api/admin/exam/paper/taskExamPage
- 请求参数：

```text
{
    "subjectId": null,  //学科
    "level": 1,  //年级
    "paperType": 6,  //试卷类型
    "pageIndex": 1,  //页面
    "pageSize": 5  
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "total": 1,
        "list": [
            {
                "id": 64,
                "name": "任务试卷五",   //试卷名称
                "questionCount": 2,   //题目总数
                "score": 60,   //试卷分数
                "createTime": "2021-08-02 14:36:26",  //创建时间
                "createUser": 2,  //创建人
                "subjectId": 1,  //学科
                "paperType": 6,  //试卷类型
                "frameTextContentId": 26  //试卷内容
            }
        ]
    }
}
```

### 4.3.19 题目分页

- 接口地址：/api/admin/question/page
- 请求参数：

```text
{
    "id": null,
    "questionType": null,
    "level": null,
    "subjectId": null,
    "pageIndex": 1,
    "pageSize": 10
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "total": 7,
        "list": [
            {
                "id": 64,
                "questionType": 5,  //题型
                "textContentId": null,
                "createTime": "2021-01-21 11:45:57",  //创建时间
                "subjectId": 1,  //学科
                "createUser": 2,  //创建人
                "score": "10", //得分
                "status": 1,  //状态
                "correct": "鹅鹅鹅， 曲项向天歌。 白毛浮绿水， 红掌拨清波。",  //标答
                "analyzeTextContentId": null,   //解析
                "difficult": 3,  //难度
                "shortTitle": "默写咏鹅"  //题干
            }
        ]
    }
}
```

### 4.3.20 题目查询

- 接口地址：/api/admin/question/select/508
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "id": 508,  //题目id
        "questionType": 5,  //题型
        "subjectId": 4,  //学科
        "title": "<p>什么是快乐星球？</p>",   //题干
        "gradeLevel": 1,  //年级
        "items": [],  //选项
        "analyze": "照抄即可",  //解析
        "correctArray": null,  //标答
        "correct": "什么是快乐星球",  //正确答案
        "score": "5",  //题目分数
        "difficult": 5,  //难度
        "itemOrder": null
    }
}
```

### 4.3.21 题目编辑

- 接口地址：/api/admin/question/edit
- 请求参数：

```text
{
    "id": 64, //题目id
    "questionType": 5, //题型
    "subjectId": 1,  //学科
    "title": "默写咏鹅",   //题干
    "gradeLevel": 1,  //年级
    "items": [],  //选项
    "analyze": "咏鹅可以带拼音",   //解析
    "correctArray": null, //标答
    "correct": "鹅鹅鹅， 曲项向天歌。 白毛浮绿水， 红掌拨清波。", //正确答案
    "score": 10,  //题目分数
    "difficult": 3, //难度
    "itemOrder": null
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": null
}
```

### 4.3.22 题目删除

- 接口地址：/api/admin/question/delete/7
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": null
}
```

### 4.3.23 任务分页

- 接口地址：/api/admin/task/page
- 请求参数：

```text
{
    "gradeLevel": null,
    "pageIndex": 1,
    "pageSize": 10
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "total": 2,
        "list": [
            {
                "id": 64,   //任务id
                "title": "中级任务",   //任务标题
                "gradeLevel": 1,  //年级
                "createUserName": "admin",  //创建人用户名
                "createTime": "2021-01-21 11:50:24",  //创建时间
                "deleted": false  //是否删除
            }
        ]
    }
}
```

### 4.3.24 任务查询

- 接口地址：/api/admin/task/select/22
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "id": 64,  //任务id
        "gradeLevel": 12,  //年级
        "title": "考试",  //任务标题
        "paperItems": [
            {
                "id": 592,  //试卷id
                "name": "考试",  //试卷名称
                "questionCount": 5,  //题目数量
                "score": 275,  //试卷分数
                "createTime": "2021-08-12 15:02:50",  //创建时间
                "createUser": 2,  //创建人
                "subjectId": 46,  //学科
                "paperType": 6,  //试卷类型
                "frameTextContentId": 2897,  //试卷内容
                "allClasses": null
            }
        ]
    }
}
```

### 4.3.25 任务编辑

- 接口地址：/api/admin/task/edit
- 请求参数：

```text
{
    "id": 64,
    "gradeLevel": 1,
    "title": "中级任务",
    "paperItems": [
        {
            "id": 64,  //试卷id
            "name": "中级任务一",  //试卷名称
            "questionCount": 5,  //题目数量
            "score": 180,  //试卷分数
            "createTime": "2021-01-21 11:49:11",  //创建时间
            "createUser": 2,  //创建人
            "subjectId": 1,  //学科
            "paperType": 6,  //试卷类型
            "frameTextContentId": 12  //试卷内容
        }
    ]
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "id": 64,  //任务id
        "gradeLevel": 1,   //年级
        "title": "中级任务",  //任务标题
        "paperItems": [
            {
                "id": 64,  //试卷id
                "name": "中级任务一",  //试卷名称
                "questionCount": 5,  //题目数量
                "score": 180,  //试卷分数
                "createTime": "2021-01-21 11:49:11",  //创建时间
                "createUser": 2,  //创建人
                "subjectId": 1,  //学科
                "paperType": 6,  //试卷类型
                "frameTextContentId": 12  //试卷内容
            }
        ]
    }
}
```

### 4.3.26 任务删除

- 接口地址：/api/admin/task/delete/1
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,  //返回状态
    "message": "成功", //返回消息
    "response": null
}
```

### 4.3.27 消息分页

- 接口地址：/api/admin/message/page
- 请求参数：

```text
{
    "sendUserName": null,
    "pageIndex": 4,
    "pageSize": 10
}
```

- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "total": 36,
        "list": [
            {
                "id": 64,   //消息id
                "title": "你好，同学！",  //消息标题
                "content": "考试请不要作弊",  //消息内容
                "sendUserName": "admin",  //发送人用户名
                "receives": "student",  //接收人用户名
                "receiveUserCount": 1,  //接收人数量
                "readCount": 1,  //已读数量
                "createTime": "2020-09-22 11:37:49" //创建时间
            }
        ]
    }
}
```

### 4.3.28 消息发送

- 接口地址：/api/admin/message/send
- 请求参数：

```text
{
    "title": "全校师生请注意",  //消息标题
    "content": "大家好",  //消息内容
    "receiveUserIds": [  //接收人
        1
    ]
}
```

- 返回参数：

```text
{
    "code": 1,  //返回状态
    "message": "成功", //返回消息
    "response": null
}
```

### 4.3.29 答卷分页

- 接口地址：/api/admin/examPaperAnswer/page
- 请求参数：

```text
{
    "subjectId": null,  //学科
    "pageIndex": 1,
    "pageSize": 10
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "total": 4,
        "list": [
            {
                "id": 64,
                "createTime": "2021-07-07 14:03:02",  //提交时间
                "userScore": "16",  //用户得分
                "subjectName": "语文",  //学科名称
                "subjectId": 1,  //学科Id  
                "questionCount": 5,  //题目数量
                "questionCorrect": 4,  //正确题目数
                "paperScore": "18", //试卷总分
                "doTime": "14 秒",  //耗时
                "paperType": 4,  //试卷类型
                "systemScore": "2",  //自动批改得分
                "status": 2,  //答卷状态
                "paperName": "限时考试二",  //试卷名称
                "userName": "student" //用户名
            }
        ]
    }
}
```

### 4.3.30 用户日志

- 接口地址：/api/admin/user/event/page/list
- 请求参数：

```text
{
    "userId": null,
    "userName": null,
    "pageIndex": 1,
    "pageSize": 10
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "total": 68,
        "list": [
            {
                "id": 64,  //日志id
                "userId": 2,  //用户id
                "userName": "admin",  //用户名
                "realName": "管理员", //真实姓名
                "content": "admin 登录了学之思开源考试系统", //日志内容
                "createTime": "2021-08-24 20:05:02" //创建时间
            }
        ]
    }
}
```

### 4.3.31 当前用户信息

- 接口地址：/api/admin/user/current
- 请求参数：无
- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": {
        "id": 64,
        "userUuid": "52045f5f-a13f-4ccc-93dd-f7ee8270ad4c", //用户uuid
        "userName": "admin",  //用户名
        "realName": "管理员", //真实姓名
        "age": 30, //年龄
        "role": 3, //角色
        "sex": 1, //性别
        "birthDay": "2019-09-07 18:56:07", //出生日期
        "phone": null, //手机号
        "lastActiveTime": "",  //最后活动时间
        "createTime": "2019-09-07 18:56:21",  //创建时间
        "modifyTime": "", //修改时间
        "status": 1, //状态
        "userLevel": null, //用户年级
        "imagePath": null  //头像
    }
}
```

### 4.3.32 用户信息更新

- 接口地址：/api/admin/user/update
- 请求参数：

```text
{
    "id": 64,  //用户id
    "userUuid": "52045f5f-a13f-4ccc-93dd-f7ee8270ad4c", //用户标识
    "userName": "admin", //用户名
    "realName": "管理员", //真实姓名
    "age": 30, //年龄
    "role": 3, //角色
    "sex": 1,  //性别
    "birthDay": "2019-09-07 18:56:07", //生日
    "phone": "11", //手机号
    "lastActiveTime": "", //最后活动时间
    "createTime": "2019-09-07 18:56:21", //创建时间
    "modifyTime": "2021-08-17 11:28:52", //修改时间
    "status": 1, //状态
    "userLevel": null, //年级
    "imagePath": null //头像
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": null
}
```

### 4.3.32 用户信息更新

- 接口地址：/api/admin/user/selectByUserName
- 请求参数：

```text
student  //用户名
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": [
        {
            "name": "student",  //用户名
            "value": 1  //用户id
        }
    ]
}
```

### 4.3.33 图片上传

- 接口地址：/api/admin/upload/configAndUpload
- 请求参数：无
- 返回参数：

```text
{
    "original": "头像.jpg",
    "name": "头像.jpg",
    "url": "http://xzs.file.mindskip.net/Fi4vlEf1ri4VMGSONwN2Ch0o8Ed_",
    "size": 19665,
    "type": ".jpg",
    "state": "SUCCESS"
}
```

### 4.3.34 个人信息修改

- 接口地址：/api/admin/user/update
- 请求参数：

```text
{
    "id": 64,
    "userUuid": "52045f5f-a13f-4ccc-93dd-f7ee8270ad4c",  //用户uuid
    "userName": "admin", //用户名
    "realName": "管理员", //真实姓名
    "age": 30, //年龄
    "role": 3, //角色
    "sex": 1, //性别
    "birthDay": "2021-09-07 18:56:07",  //出生日期
    "phone": "2112112", //手机号
    "lastActiveTime": "", //最后活动时间
    "createTime": "2019-09-07 18:56:21",  //创建时间
    "modifyTime": "2021-08-31 10:08:03", //修改时间
    "status": 1, //状态
    "userLevel": null,  //年级
    "imagePath": null //头像
}
```

- 返回参数：

```text
{
    "code": 1,
    "message": "成功",
    "response": null
}
```
