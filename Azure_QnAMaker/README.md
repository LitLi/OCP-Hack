# 基于QnA Maker的问答机器人
这个实验会介绍如何使用QnAMaker轻松创建一个问答帮助机器人的服务，并使用Azure Bot Services集成该QnA服务实现一个可以在Skype/Web沟通的机器人样例。本样例主要包括以下几部分内容：
- 创建QnA服务
- 创建问答机器人Bot Service
- 集成开发问答机器人集成QnA服务
- 注册发布问答机器人
- 测试问答机器人
  
## 实验条件
1. 需要有Microsoft Azure国际版订阅
2. 需要下载[Bot Emulator](https://github.com/Microsoft/BotFramework-Emulator/releases/tag/v4.3.0)
3. 需要[Visual Studios 2017](https://visualstudio.microsoft.com/zh-hans/downloads/?rr=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fazure%2Fbot-service%2Fbot-builder-tutorial-basic-deploy%3Fview%3Dazure-bot-service-4.0%26tabs%3Dcsharp)以上版本


## 创建QnA服务
QnAMaker可以让开发者使用FAQ URL，FAQ文件或者手工录入问题答案等方式，轻松构建一个问答机器人服务。

1. 使用Azure订阅账号登陆[Azure Portal](http://portal.azure.com)，选择+，创建资源，搜索QnAMaker，选择搜索出来的QnA Maker服务，点击Create。
   
   <img width="300" height="300" src="./images/image101.JPG"/>
2. 输入QnA Maker服务的名字，选择订阅，价格，部署地理位置等信息； 其中价格可以选择S0（提交的问题对文档不限量，每月10美金）；Search Price可以选择F(3 Indexes)；本实验不需要监控服务使用情况，可以将App Insights服务Disable，点击Create。
   
   <img width="300" height="600" src="./images/image102.JPG"/>

   创建完成后，就可以开始QnA Maker应用的创建和训练了。
3. 使用Azure订阅账号登陆[QnAMaker门户](http://qnamaker.ai)，点击Create a knowledge base，在第二步中选择你的Azure订阅和你刚刚创建的QnAMaker的服务，输入Knowledge Base的名字，输入你要训练的[问题对文件](./src/qna.txt)，点击Create。
    <img width="500" height="300" src="./images/image103.JPG"/>
    <img width="500" height="300" src="./images/image104.JPG"/>
4. KnowledgeBase创建完成后，问题对编辑和训练界面， 可以检查一下导入的文件是否问题对显示正确（样例中有11个问题对），确认后，点击Save and train，进行训练。
   <img width="600" height="350" src="./images/image105.JPG"/>
5. 训练完成后，可以点击Test，进行测试， 输入你需要提问的内容，回车。点击inspect，可以看到后台给出的具体分析，确认问题回答的匹配程度。不满意，可以选择增加或修改答案，然后重新Save and train。直到满意。
   <img width="600" height="350" src="./images/image106.JPG"/>
6.训练和测试完成后，可以点击Publish，发布应用，发布成功后需要保存其中的**Knowledge BaseID，Endpoint key，和hostname**，后面会用到。

   <img width="600" height="350" src="./images/image107.JPG"/>