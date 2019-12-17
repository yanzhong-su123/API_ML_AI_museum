# 项目名称：博物馆
# Product Requirement（产品说明文档）

| Title                     | Content |
| ------------------------- | ------- |
| Target release(发布日期)  | 2019/12 |
| Epic(史诗名称)            | 宜动且宜静  |
| Document status(文档状态) | 进行中  |
| Document owner(文件主人)  | 苏衍中 |
| Designer(领头的设计师)    | 苏衍中 |
| Developer(领头的开发者)   | 苏衍中 |
| QA(领头的测试者)          | 苏衍中 |

# 价值主张设计
   基于百度AI上的人体检测api来先区分正常用户和患有多动症或者身障者人群，再根据人体关键点的识别来集成一套数据资料（大数据），从而在调用其API时可以准确的推测和判断不同的类型人群遇到了什么困难和危险；同时调用百度AI中的语音识别和合成与呼叫中心实时语音识别来为身障者提供额外的语音交互服务，通过为其提供小的麦克风与馆内服务人员的智能语音连接（用完需回收）或者是自己的电话来呼叫馆内帮助中心，帮助正常人、身障者或多动症可以及时向馆里的人员进行求助或咨询。

## 加值宣言
- 简洁性：通过人体检测api，检测图像中的所有人体，标记出每个人体的坐标位置；不限人体数量，适应中低空斜拍、人体轻度遮挡、截断等场景检测图像中的所有人体，识别人体的20余类通用属性，包含性别年龄、服饰类别、服饰颜色、佩戴物、行为动作来简单区分不同人群
- 实用性：通过人体关键点api，检测图像中的人体并返回人体矩形框位置，精准定位21个核心关键点，包含头顶、五官、颈部、四肢主要关节部位，支持多人检测、大动作等复杂场景，但发现个人行为所被检测到的关键点异常，并保持超过三分钟，则判定个人可能需要帮助或者遇到危险，以便帮助特殊人群提供及时的服务。
- 效率为先：通过智能语音识别和合成与呼叫中心实时语音识别的调用，在个人通过电话或其他智能语音方式来与馆员互动，然后采用针对呼叫中心场景专门训练的语音识别模型，将电话语音实时精准识别为文字，若文字中仅为寻求馆里的信息，可接入馆员提前录好的语音，假设仍有不明白的问题，请转人工服务。而对于紧急的求助，快速连接到在线的馆员，并实时监测情况，防止突发事件的发生。   

## 核心价值（最小可行性产品）
- 1.基于用户的最基本需求，为馆员便捷地去区分不同人群，以实现更好的管理和服务
- 2.检测身障者的动作行为，及时分析并监测其是否需要帮助或其他的危险求助
- 3.监测多动症患者的关键部位，一旦出现异常可及时让其获得必要的帮助，同时智能语音交互可帮助馆员迅速得知紧急情况，让患者的问题得到有效地处理。
- 4.基于不同人群的语音求助的需求，提供语音识别和呼叫中心平台的实时语音交互，为身障者和多动症人群提供更多可行的服务。

## 背景：
博物馆人流量较大，来访的游客鱼龙混杂，其中身障者和多动症人群作为一种比较特殊的人群，对于他们的一些特殊的需求，若当我们考虑不周全的话，会发生一些意外的不良情况甚至危险，同时我们也需要为特殊人群的陪伴者提供更加便捷的服务。

## 设计目的：
- 对于参观者：切实维护身障者和多动症人群的权益，给予他们提供更加舒心的服务，并且及时地监测到他们的实时情况，然后对其进行帮助和解决实际的问题。
- 对于馆员：提供一个更加智能的语音交互平台，帮助馆员更好地接待特殊人群，让他们可以享受和正常人一样无差别的观赏服务。

## 用户定位：
***参考并浏览博物馆展览的身障者和多动症人群，还有其陪伴人员***

## 用户痛点：
- 1.身障者可能存在肢体行动不便、听力或其他方面的能力缺失，导致他们不能独自完成在参观博物馆中出现的种种问题，例如不能便捷地找到电梯的出入口、或不能听懂别人的协助意见，以致无法感到较好的参观体验。
- 2.身障者的陪同人在既要看管好身障者同时，又要急于求助馆员的情况，可能两种条件无法兼顾。
- 3.多动症人群的行为动作可能会较多且异常，情绪波动较大，需要受到馆员的更加留心的监测，以防突发情况的发生而不能及时解决。

## 应用场景：
- 1.进入馆里，先通过人体检测和关键点提供智能分析，区分不同人群；
- 2.为身障者和多动症人群提供智能的求助设备，让陪同人和自己能够及时地求助馆员

## 用户需求：
**所使用的人工智能对应其需求列表**
| 用户需求 | 对应的人工智能 | 重要程度 |
| --- | --- | --- |
| 听觉上存在障碍的人难以听到馆员对展览展品的介绍	| 智能语音识别和合成api可以返回对展览的具体文字介绍 | 中 |
| 行动不便的人群不知厕所在哪，需要请求帮助	| 智能对话平台根据他对需要提供及时的路线语音反馈（包括路线文字反馈）| 低 |
| 多动症人群被监测到自己的多次触摸不可摸的展品 | 人体关键点监测实时反馈数据给语音平台，而在线馆员及时到场进行引导和制止其行为，对其后续行为继续监控 |高 |
