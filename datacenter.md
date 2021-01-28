# 楼查查数据中心表结构文档

>  拟定按月更新数据  
>  区划最小标准颗粒 街道(乡镇)  颗粒最小尽量做到社区  
>  由于数据分析区划颗粒度到街道，所以建议每条数据都以标准街道代码为主， 城市做对用的SUM处理  

+ ## 分析
1. 项目统计
2. 本月新增
3. 土地性质
4. 项目类型(住宅、商业、公寓、其他)
5. 产权情况
6. 建成年份(老旧、新存、新建)
7. 建筑形态
8. 项目户数
9. (新房、二手房、租赁、法拍房、土地)挂牌量、成交量、成交率 按月更新
10. 新房成交均价
11. 新房成交户型结构
12. 新房成交年龄结构
13. 房屋套数 (年)
14. 人口数量 (年)
15. 人均住房面积 (年)
16. 本地人口、流动人口购房、租赁比例
17. 住房消费 按年更新
+ ## 来源分析
1. 项目统计->小区表(月)
2. 本月新增->小区表(月)
3. 土地性质->小区表(月)
4. 项目类型->小区表(月)
5. 产权情况->小区表(月)
6. 建成年份->小区表(月)
7. 建筑形态->楼幢表(1-6,7-12,13-)(月)
8. 项目户数-> 小区->房屋表(1-500, 501-2000,20001-5000,5001-)(月)
9. (新房、二手房、租赁、法拍房、土地)挂牌量、成交量、成交量  (月)  
10. 新房成交均价->  (月)
11. 新房成交户型结构
12. 新房成交年龄结构
13. 房屋套数->房屋表
14. 人口数量->人口普查+出生率+死亡率(人口变化表按年+市)
15. 人均住房面积-> 住房总面积(----)/人口数
16. 本地人口、流动人口购房、租赁比例
17. 住房消费->平均房屋总价/人均年收入(市+年)
+ ## 表结构分析

### 区划编码表(district_code)
|编号|字段名|类型|备注|
| ----: | :--- |:-- |:--- |
| 1 | id | int | Id 备注编码版本 |
| 2 | pid | int | 等级父Id |
| 3 | code | bigint | 编码 |
| 4 | name | varchar(100) | 行政名 |
| 5 | level | tinyint | 等级1，2，3，4，5 |
| 6 | status | tinyint | 状态 | 
| 7 | url | varchar(255) | 临时抓取数据用 |
| 8 | is_read | tinyint | 临时抓取数据用 |


### 基础信息统计表-按照街道(data_month)
| 编号 | 字段名 | 类型 | 备注 |
| ----: | :--- |:-- |:--- |
| 1 | id |int(11)| Id |
| 2 | city |char(4)| 城市 |
| 3 | district |char(6)| 区县 |
| 4 | street |char(9)| 街道 |
| 5 | year | year| 年 |
| 6 | month | tinyint | 月 |
| 7 | community_num | int | 项目数量 |
| 8 | build_num | int | 楼幢数 |
| 9 | community_add | int | 本月新增数量 |
| 10 | global_land | int | 国有土地项目数 |
| 11 | private_land | int | 集体土地项目数 |
| 12 | zz_proper_type | int | 项目类型住宅数 |
| 13 | sy_proper_type | int | 项目类型商业数 |
| 14 | gy_proper_type | int | 项目类型公寓数 |
| 15 | qt_proper_type | int | 项目类型其它数 |
| 16 | have_right_nature | int | 有证项目数量 |
| 17 | no_right_nature | int | 无证项目数量 |
| 18 | community_old | int | 老旧小区数量(2000年前项目数量) |
| 19 | community_new | int | 新存小区(2000年后项目已交房项目数量) |
| 20 | community_ing | int | 新建小区(2000年后未交房项目数量) |
| 21 | build_floor_o | int | 建筑形态1-6一等级 楼幢数量 |
| 22 | build_floor_t | int | 建筑形态7-12二等级 楼幢数量 |
| 23 | build_floor_th | int | 建筑形态12以上三等级 楼幢数量 |
| 24 | community_house_o | int | 项目户数第一等级500以下小区数量 |
| 25 | community_house_t | int | 项目户数第一等级501-2000小区数量 |
| 26 | community_house_th | int | 项目户数第一等级2001-5000小区数量 |
| 27 | community_house_f | int | 项目户数第一等级5001以上小区数量 |
| 28 | land_online | decimal(20,2) | 土地挂牌量 |
| 29 | land_finish | decimal(20,2) | 土地成交量 |
| -- | land_floor_price | decimal(6,2) | 楼面地价 |
| -- | land_premium_rate | decimal(6,2) | 溢价率率 |
| 31 | newhouse_online | int | 新房挂牌 |
| 32 | newhouse_finish | int | 新房成交量 |
| 33 | newhouse_finish_price | decimal(12,2) | 新房成交均价 |
| 34 | newhouse_rate | decimal(6,2) | 新房成交率 |
| 35 | house_finish_tow_apartment | int | 房屋成交二居室户型数量 |
| 36 | house_finish_three_apartment | int | 房屋成交三居室户型数量 |
| 37 | house_finish_four_apartment | int | 房屋成交四居室户型数量 |
| 38 | house_finish_other_apartment | int | 房屋成交其它居室户型数量 |
| 39 | house_finish_one_age | int | 房屋成交年龄结构数量 一等级20岁以下 |
| 40 | house_finish_two_age | int | 房屋成交年龄结构数量 二等级21-30岁|
| 41 | house_finish_three_age | int | 房屋成交年龄结构数量 三等级31-45岁|
| 42 | house_finish_four_age | int | 房屋成交年龄结构数量 45岁以上|
| 43 | eshouse_online | int | 二手房挂牌 |
| 44 | eshouse_finish | int | 二手房成交 |
| -- | erhouse_online_price|decimal(12,2)|二手房挂牌均价|
| -- | sfhouse_online | int | 司法拍卖挂牌数量 |
| -- | sfhouse_finish | int | 司法拍卖挂牌数量 |
| -- | sfhouse_online_price | decimal(12,2) | 司法拍卖挂牌均价 |
| 47 | zlhouse_online | int | 租赁挂牌 |
| 48 | zlhouse_finish | int | 租赁成交 |
| -- | zlhouse_online_price |decimal(12,2)|租金均价|
| 49 | create_time | datetime | 添加时间 |
| 50 | up_time | datetime | 更新时间 |


### 基础信息统计表-按照城市(data_year)  更新年

| 编号 | 字段名 | 类型 | 备注 |
| ---: | :--- |:--- |:--- |
| 1 | id | int(11) | Id |
| 2 | city | char(4) | 城市 |
| 3 | year | year | 年 |
| 4 | house_num | int | 房屋套数 |
| 5 | population | int | 人口数量(按照城市存储) |
| 6 | per_capita_income | decimal(8,2) | 人均收入(计算住房消费) |
| 7 | house_price | decimal(12,2) | 城市房屋均价(计算住房消费) |
| 8 | local_mai | decimal(4,2) | 本地人口购房占比 |
| 9 | flow_mai | decimal(4,2) | 流动人口购房占比 |
| 10 | local_zu | decimal(4,2) | 本地人口租房占比 |
| 11 | flow_zu | decimal(4,2) | 流动人口租房占比 |
| 12 | create_time | datetime | 添加时间 |
| 13 | up_time | datetime | 更新时间 |


### 小区附加信息表(data_community140000)
| 字段名 | 类型 | 备注 |
| :--- |:--- |:--- |
| id | int | Id |
| city | char(4) | 城市 |
| com_id | int | 小区Id |
| year | year | 年 |
| month | tinyint | 月 |
| sell_price | decimal(8,2) | 小区成交均价 |
| rent_price | decimal() | 小区租赁均价 |
| xq_index |tinyint|小区综合指数|
|jg_index|tinyint|价值指数|
|pz_index|tinyint|品质指数|
|bl_index|tinyint个|便利指数|
|rd_index|tinyint|热度指数|
|ss_index|tinyint|舒适指数|
|sell|int|出售挂牌|
|joint_rent|int|合租|
|sell_rate|decimal(6,2)|出售成交率|
|rent|int|出租挂牌|
|rent_rate|decimal(6,2)|出租成交率|
|good|int|赞|
|bad|int|踩|
| create_time | datetime | 添加时间 |
| up_time | datetime | 更新时间 |


### TODO
### 公司表需要添加一个通俗名字字段
### 开发通俗表--关联项目



<br />

---

# 楼查查算法文档

+ ## 采光算法 (不变)
+ ## PM2.5算法 (天)
+ ## 小区综合指数 (月更新)
    `综合指数 = 价值指数*25% + 品质指数*10% + 舒适指数*20% + 便利指数*30% + 热度指数*15%`
+ ## 价值指数
    `价值指数 = 出售指数 * 50% * (1 ± 区划出售价格涨跌率) + 出租指数 * 50% * (1 ± 区划出租价格涨跌率) `  
    出售指数= ((本项目价格 - 同城最小价格) / (同城最大价格- 同城最小价格) * 100 ) * (1 ± 区涨跌率)   
    出租指数= ((本项目价格 - 同城最小价格) / (同城最大价格- 同城最小价格) * 100 ) * (1 ± 区涨跌率) 
    > 本项目成交均价、本城市成交最大、最小价格、区县涨跌率  
    > 本项目出租均价、本城市出租最大、最小价格、区县涨跌率
+ ## 品质指数
    `品质指数 = 30%开发企业 + 35%物业公司  + 15%建筑结构 +  20%户数`  
    开发企业 = (本企业关联项目数 - 关联项目数最小(一般为1)) / (本城市关联项目数最多-项目书最少(1)) * 100 + 开发企业附加值  
    物业公司 = (本公司关联项目数 - 关联项目数最小(一般为1)) / (本城市关联项目数最多-项目书最少(1)) * 100 + 物业公司附加值  
    建筑结构  
    |建筑结构|分值|
    |:---|---:|
    |钢结构|90|
    |钢筋混凝土|80|
    |砖混|70|
    |其它(砖木结构等)|60|  

    
    户数 = (本项目户数-本城市最小户数) / (本城市最大户数 -  本城市最小户数) * 100
+ ## 舒适指数
    `舒适指数 = 30% 容积率 + 30% 绿化率 + 40% 出租合租率`
    > 容积率先求倒数  
    > 出租合租率求倒数

    容积率 = (本项目- 城市最小) / (城市最大-城市最小) * 100  
    绿化率 = (本项目-城市最小) / (城市最大-城市最小)  * 100  
    出租合租率= (本项目-城市最小) / (城市最大-城市最小)  * 100  
+ ## 热度指数 
    `热度指数 = 60%出售、出租、挂牌量、成交率 + 20%用户搜索 + 20% 用户评分`
    > 用户搜索率 = 上个月该项目搜索数/总用户搜索数  
    出售、出租、挂牌量、成交量指数 = 分别计算4个求均值
    
    出售、出租、挂牌、成交 = (本项目-城市最小) / (城市最大-城市最小)  * 100  
    用户搜索指数 = (本项目- 城市最小) / (城市最大-城市最小) * 100   
    用户评分 = 基准分 50 + (本赞踩差-最小赞踩差）/（最大赞踩差-最小赞踩差)*50
    
+ ## 便利指数

---
> ## 开发商附加值表



