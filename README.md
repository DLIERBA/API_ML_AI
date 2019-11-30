### 毕业纪念APP 

#### 一.加值宣言 
经调查，目前已有较多的帮助用户制作相册、制作短视频类的APP，例如Quick、微剪辑、右糖、爱美刻等。然而用户的需求在不断地变化，用户对于毕业纪念APP的要求不再仅仅只是制作制作相册或短视频，用户希望毕业纪念APP能够拥有更多的人性化便捷化的功能。
因此，我构想的毕业纪念APP的功能有：
1. 当用户站在教学楼前拍照留念时，可能会突然想起刚入学时拍下的那张照片，并且想要将那张「过去时光的照片」中的自己与现在的自己进行同框对比，但可能由于各种原因无法实现。因此我设想APP内应该有一个功能，利用人像分割功能，然后可以使用户「过去时光的照片」中的自己出现在应用中的取景器中，与眼前的场景重叠，然后合成出一张「今昔对比」的照片。
2. 我相信很多人都曾经历过在路上遇到了一个似曾相识的朋友却突然忘记她/他名字的尴尬情况。因此我设想在APP内增加一个功能，导入他/她现在的一张照片，然后通过人脸搜索，进行人脸搜索后，会出现他/她在学校的一些讯息，例如姓名、年级、专业等。
3. 根据用户的地理定位，以地图的形式显示在他/她附近有哪些同学，然后用户可以点击地图上显示的同学头像进入聊天框进行聊天。同时，如果想和老同学聚会，APP还能根据两者的地理定位，推荐一个距离两者都较近的餐厅。

#### 二.核心价值 （最小可行性产品）

着眼于用户想将现在的自己与过去的自己进行对比的需求

#### 三.背景
目前，对于毕业纪念APP的这一概念，很多人认为就是为用户提供简易制作毕业纪念相册或毕业纪念视频的功能软件。因此想要从市场中脱颖而出，就要另辟蹊径，满足用户更加多样化的需求。

#### 四.目的 
1. 让用户轻松实现「今昔对比」
2. 避免偶遇老同学却不知对方姓甚名谁的尴尬情况
3. 增加一个联系老同学的方法
4. 解决想组织同学聚会，却不知道应该将聚会地点定在哪里的问题

#### 五.目标 
+ 前期目标
实现「今昔对比」功能：用户将旧照片导入APP内，APP能够智能地将旧照片中的人像抠下来，并且抠下来的人像能够直接出现在应用中的取景器中，与眼前的场景重叠，然后生成一张对比图。

+ 中期目标
实现人脸搜索功能：用户将需要识别的同学（朋友）的照片导入APP内，APP能够智能地进行人脸搜索，搜索成功后将会出现被识别同学的一些在校的相关信息。

+ 后期目标
     1. 建立一个老同学社交圈：可以帮助用户发现他/她的周围分布着哪些老同学以及距离多远，并且还能提供沟通交流的基本服务。
     2. 协助用户组织聚会：根据用户与老同学们的地理定位，为用户推荐最佳的聚会地点，距离两者都不会太远。

#### 六.用户
1. 应届毕业生
2. 非应届毕业生（就已经毕业了一段时间）

#### 七.用户痛点 
+ 场景一：用户想在同一地点，让过去的自己与现在的自己同框对比。
+ 场景二：在路上遇到了一个似曾相识的朋友却突然忘记她/他名字的尴尬情况。
+ 场景三：想联系旧同学，但又没有她/他的联系方式
+ 场景四：想组织同学聚会，但却不知道选择在哪个位置的聚会地点比较合适

#### 八.用户需求:（使用的人工智能要反映到需求列表中） 
|用户案例|对应标题|重要程度|
|:-|:-:|-:|
|用户想实现今昔对比|人像分割|重要|
|用户想知道老同学的信息|人脸搜索|重要|
|用户想了解老同学的地理分布情况|地理围栏|次重要|

#### 九.使用者交互与设计（axure产品原型）


#### 十.产品结构图


#### 十一.API 的运用 
1. 百度API——人脸搜索
+ HTTP方法：POST
+ 请求URL： https://aip.baidubce.com/rest/2.0/face/v3/search
+ API价值主张
①支持百万级规模的人脸库管理和搜索，检索速度业内领先
②提供可视化人脸库管理功能，支持人脸组、用户、人脸维度的增、删、改、查操作
③提供在线的人脸搜索接口、人脸库管理组合接口，可以快速集成，达到百万人脸库毫秒级检索速度，实现黑白名单自定义匹配等功能
④提供一体机和软件部署包两种私有化方案，支持百万级人脸库精准查找，毫秒级搜索结果响应，适用于安防、监控等场景

+ 请求代码示例
    ```
       # encoding:utf-8

import requests

'''
人脸搜索
'''

request_url = "https://aip.baidubce.com/rest/2.0/face/v3/search"

params = "{\"image\":\"027d8308a2ec665acb1bdf63e513bcb9\",\"image_type\":\"FACE_TOKEN\",\"group_id_list\":\"group_repeat,group_233\",\"quality_control\":\"LOW\",\"liveness_control\":\"NORMAL\"}"
access_token = '[调用鉴权接口获取的token]'
request_url = request_url + "?access_token=" + access_token
headers = {'content-type': 'application/json'}
response = requests.post(request_url, data=params, headers=headers)
if response:
    print (response.json())

    ```
2. 百度API——人像分割
+ HTTP 方法：POST
+ 请求URL： https://aip.baidubce.com/rest/2.0/image-classify/v1/body_seg
+ API价值主张
①将原始图片中的人像分离出来，选择新的背景图像进行替换、合成
②人像分割算法业界领先
③支持返回分割后的二值图、灰度图、人像前景图，并可通过参数设置，自主设置返回哪些结果图，避免造成带宽浪费


3. 高德API——地理围栏
+ API价值定位

#### 十二.AI产品概率性 
百度人脸搜索的特色优势
+ 支持百万级规模的人脸库管理和搜索，检索速度业内领先，可应对各种业务需求
+ 提供可视化人脸库管理功能，支持人脸组、用户、人脸维度的增、删、改、查操作
+ 提供企业级稳定、精确的大流量服务，拥有毫秒级识别响应能力、弹性灵活的高并发承载，可靠性保障高达99.99%
+ 基于百度专业的深度学习算法和海量数据训练，人脸识别算法在最权威的公开评测比赛中排名世界领先

#### 十三.API使用风险评估


+ 错误现象处理方法
① 当人脸识别错误的时候，可以把用户上传的照片存入数据库内，并请求用户填写反馈信息，以帮助机器学习。
② 当人脸识别失败的时候，就用人性化的语气提示用户。第一次识别错误：‘人家好像近视了，没办法看清这帅气脸庞，能请主人再给一次机会，上传清晰的图片吗？’；第二次识别错误：‘哎呀，我可能太笨了，请主人发送反馈留言，后台客服妹妹将为您亲自解答。’

#### 产品的可行性
1. 该产品是一个APP
+ App可以实现完整功能，灵活性强
+ APP能够在交互、视觉等用户体验上满足用户的高要求
+ App的界面内容更丰富，运转速度快，系统更加流畅

2. 该产品需求明确，而且需求针对的特定的群体普遍偏年轻，其优势就是年轻群体对新鲜事物的接受度较高且具有较强的传播能力

3. 该产品有核心功能和辅助功能，功能多样而且新颖

4. 该产品能有效解决用户日常生活中较为常见的尴尬情况，

#### 交互需求 
1. 当涉及到下载或其他很耗费流量的操作时，会进行2G/3G网络还是wifi网络的判断，当判断出是非wifi时，会进行提醒。其他需要向后台请求数据时，只进行简单的网络状况是否良好的判断，当网络状况不良时进行提示。
2. 当用户上传的图片不符合要求时，会提醒用户重新上传
#### 异常流
如果计算卡路里不成功，给出具体字段的错误提示信息，让用户重新调整好光亮度和角度重新拍摄；
如果拍照识别的菜品不正确，提示用户可以手动选择和更改。
如果用户不满意个性化推荐的食谱，弹出更换提示。
#### 非功能性需求
+ 性能：估计用户数为1万人，每天登录用户数为3000左右，网络的带宽为100M带宽。在非高峰时间根据编号和名称特定条件进行搜索，可以在3秒内得到搜索结果。当通过互联网接入系统的时候，期望在编号和名称搜索时最长查询时间<15秒。
+ 可靠性：要求系统7x24小时运行，全年持续运行故障停运时间累计不能超过10小时。
+ 可维护性：故障的可排查能力，系统的修正，升级，备份，恢复机制。
+ 安全：当用户的账号在常用设备以外的设备登录了，要及时发消息通知用户；当用户出现登录异常的情况时，要开启动态口令验证（例如短信发生动态码）等。
+ 易用性： 功能操作简单，界面清晰简洁，某些较复杂的操作需要给用户提供操作指引。
+ 数据一致性：当发生用户个人资料变更时，保证其他地方的信息要被同步修改。
#### 结果预期
+ 上线初期，先在一个小区域内（例如某个地区的高校）进行推广，然后收集这一部分使用者的体验评价，根据情况进行完善
+ 当APP功能基本完善，用户评价普遍向好时，面向整个市场推出使用，不过刚开始需要使用一些奖励措施，吸引更多的用户使用APP
+ 到APP被广泛应用，拥有较为稳定的用户群体时，可减少甚至取消先前为了吸引新用户所采取的奖励，并且可以考虑增加其他功能，利用持续创新的手段吸引新用户以及留住旧用户
+ 发展到一定阶段后，APP可能会接手广告业务获利；或者在APP内开设购物功能，贩卖毕业用品之类的；也有可能选择增设会员服务，以吸引用户在APP内消费，最终实现APP盈利
#### 附录
