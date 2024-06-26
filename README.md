# 基于 VBA 和 Python FastAPI 的 Excel 在线评分系统

可以实现多个评委对多个机构的实时打分和自动汇总，评委和机构名称可配置

## 使用方法

### 客户端

#### 基本用法

将“评分汇总.xlsb”复制到每个评委的电脑上

每个评委都按照以下步骤评分：
1. 打开“评分汇总.xlsb”
2. 点击“开始评分”按钮，输入姓名
3. 对当前部门进行评分
4. 评分完成后，点击“下一个”按钮，继续对下一个部门评分
5. 当完成所有部门的评分后，点击”提交”按钮

同时，将“评分汇总.xlsb”复制到汇总者的电脑上，汇总者按照以下步骤进行汇总：
1. 打开“评分汇总.xlsb”
2. 点击“汇总评分”按钮
3. 等待所有评委完成打分
4. 点击完成按钮，程序将自动计算平均分，并将汇总表保存在与“评分汇总.xlsb”同目录下的“汇总表.xlsx”中

#### 自定义
* 若需修改所需评价的部门，只需编辑“评分汇总.xlsb”中的部门名称即可
* 若需增加评委，只需将“评分汇总.xlsb”复制到新增评委的电脑上让该评委打分即可

### 服务器

输入如下命令启动评分汇总服务器：
```
python server.py
```
默认监听 5422 端口

## 原理

客户端与服务器间通过 WebSocket 长连接进行双向数据传输，实现评分数据的上传和下载。

由于 VBA 原生并不支持 WebSocket，所以使用 VBA 包装 Windows 的 WinHTTP API，并在此基础上实现 WebSocket 连接。