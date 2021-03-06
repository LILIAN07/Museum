# 易览产品需求文档

文档名称 | 博物馆产品需求文档
---|---
文档状态 | 进行中
产品名称 | 易览
文档作者 | 连盈
发布日期 | 2019.12.26

## 价值主张
### 相关背景
> **小件文物**一般包括小型青铜器、小型玉器、书画作品等，以上几种文物，由于体型较小，故此可以由一个人进行搬运。

> **中型文物**中型文物包括陶瓷制品、桌椅家具、青铜器具等。由于器物本身非常脆弱，因此一个人搬运风险极高，必须要两个人合作搬运才行。

> **大型文物**大型文物一般历史价值较高，而且样式、大小差别很大，要根据具体情况划分人员搬运。

* 各类文物的搬运转移有着不同守则，现在许多博物馆都是沿用最基础的纸质版或者电子版表格进行人员调配，而这些往往都是人工排班。

* 博物馆的许多藏品锁都是使用基础的钥匙锁，钥匙容易丢失或被复制，安全性不强。

* 博物馆员工基本都可以通过网络查找本馆藏品名录，但是往往需要登录专属的网站，查看信息便捷度不强。

### 加值宣言
* 市面有观览智能指引APP，但基本没有针对性帮助博物馆工作人员保存、转移展品的APP。易览可以录入文物类型信息，根据事先划分好的准则进行人员调配，将展区位置信息与藏区位置信息联系，指引员工高效转移展品，方便高效。

* 易览支持人脸识别功能，重要展品按照博物馆要求划分1-3人共同负责，需按流程完成所有负责人的面容信息识别，并通过活体检测是否为真人（抵御照片、视频3D模具）后才能解锁。
（考虑到面容锁的成本，先试用于含贵重展品的大型博物馆）

### 核心价值
为博物馆工作人员根据不同文物类型划分负责人，并进行排班，提示藏区向展区的转移路线供工作人员参考，并通过（多人）人脸识别、活体检测解锁展品，保证展品安全。

## 用户分析
### 目标用户
博物馆进行展品转移的工作人员

### 用户痛点
* 根据展品类型划分负责的工作人员考量因素多，排班效率低。
* 转移展品过程中展品安全保障较少，展品出现问题寻找责任人效率低。
* 搬运展品过程中再找出钥匙开锁比较麻烦，且钥匙容易丢失。

### 需求分析
使用案例 | API的使用| 重要等级
---|---|---
根据展品信息划分负责人员，进行排班 |---| 次要
（多人）面部识别解锁重要展品 |人脸识别、活体检测| 重要
 联系展品的展区及藏区指示转移路线 |室内地图| 重要

## 原型
### 基本信息
* [原型查看](http://nfunm043.gitee.io/bowuguan/)
* [原型下载](http://gitee.com/NFUNM043/bowuguan)

### 原型展示
![首页](https://images.gitee.com/uploads/images/2019/1225/004020_d128c7ac_1831462.png "首页.png")
![认证](https://images.gitee.com/uploads/images/2019/1225/004045_4dbb184a_1831462.png "认证.png")
![负责人](https://images.gitee.com/uploads/images/2019/1225/004059_26598772_1831462.png "负责人.png")
![查询](https://images.gitee.com/uploads/images/2019/1225/004109_461c2561_1831462.png "查询.png")
![位置](https://images.gitee.com/uploads/images/2019/1225/004122_32b27727_1831462.png "位置.png")
![我的](https://images.gitee.com/uploads/images/2019/1225/004135_0664e0b4_1831462.png "我的.png")
![客服](https://images.gitee.com/uploads/images/2019/1225/004142_361d6901_1831462.png "客服.png")
![反馈](https://images.gitee.com/uploads/images/2019/1225/004150_8a3867ca_1831462.png "反馈.png")

## API的选择与使用
### 使用水平
**人脸识别**

在转移展品的过程中，一人或多人按APP流程完成面容信息认证即可解锁展品。

         # encoding:utf-8
         import requests 
         
         # client_id 为官网获取的AK， client_secret 为官网获取的SK
         host = 'https://aip.baidubce.com/oauth/2.0/token?grant_type=client_
         redentials&client_id=【官网获取的AK】&client_secret=【官网获取的SK】'
         
         response = requests.get(host)
         if response:
         print(response.json())

**活体检测**

在转移展品的过程中，出了基础的人脸识别认证，还会进行活体认证，以防不法分子盗用工作人员的照片、视频甚至制作3D模型窃取展品。

         # encoding:utf-8
         import requests 

         # client_id 为官网获取的AK， client_secret 为官网获取的SK
         host = 'https://aip.baidubce.com/oauth/2.0/token?grant_type=client_credentials&client_id=【官网获取的AK】&client_secret=【官网获取的SK】'
         
         response = requests.get(host)
         if response:
         print(response.json())


**室内地图**

为转移展品的员工定位展区和藏区，并智能规划路线，指示员工高效完成工作。[相关介绍页面](http://lbsyun.baidu.com/products/products/indoor)
