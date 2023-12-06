## 结构力学求解器cumt
### 单位统一为：长度mm，力N，应力MPa，默认E=206000MPa ，角度默认 °（逆时针为正），角度为整体坐标系下角度
### 杆件除角度外，其余参数按局部坐标系输入
### 力按整体坐标系输入

#力的类型暂定为
- 0：节点力  
- 1：节间力  
  -  0：集中力  
  -  1：集中力矩  
- 3：均布力，需要补充长度（分数表示）、起点长度和终点长度[均布力距离起点的长度，均布力距离终点的长度]和端点值[起点值，终点值]

力的角度为整体坐标系下的角度


***杆件索引使用杆件的编码不使用节点编码！！！***

***中间过程的数据交换尽量使用json，并确认（ensure_ascii=False, encoding='utf-8'）这两项参数以保证中文的正确显示可可读性。***

**计算程序读取杆件gan_jian_lib.json。序号、节点(类型为列表)为必须参数，杆件角度或三角函数值二选一。**   

**杆件连接类型：‘lei_xing’:**
- 0：刚接
- 1：铰接
- 2：x轴向自由的定向连接
- 3：y轴向自由的定向连接
- 4：自由端
- 支座：
- 10：固定支座
- 11：固定铰支座，弯矩自由
- 12：定向支座，x轴自由
- 13：定向支座，y轴自由
- 14：某某支座，限制弯矩
- 15：铰支座，限制x轴
- 16：铰支座，限制y轴


**杆件输入规范（存储于gan_jian_lib.json）：**  
输入的值的优先级，是高于设置中的默认值的优先级。设置中的默认参数全局生效。  
关于角度输入，当且仅当cos和sin均为默认值，即cos=sin=0时，才会采用角度a。
- xu_hao=0        ##杆件编号，从0开始，依次递增
- jie_dian=[0,0]  ##节点编号，从0开始，建议依次递增
- lian_jie=[0,0]  ##杆件两端连接类型，详见《杆件连接类型》，必须与'节点'对应
- E=206000        ##弹性模量，默认206000Mpa
- A=1             ##杆件截面积，默认1mm^2
- I=1             ##杆件截面惯性矩，默认1mm^4
- L=1             ##杆件长度，默认1mm
- a=0             ##杆件局部坐标系和整体坐标系夹角，建议（0°，180°）
- cos=0           ##杆件局部坐标系和整体坐标系夹角余弦值
- sin=0           ##杆件局部坐标系和整体坐标系夹角正弦值  
范例：  
[
    {'xu_hao':0,'jie_dian':[0,1],'lian_jie':[0,0],'E':206000,'A':1,'I':1,'L':1,'a':0,'cos':0,'sin':0},  
    {'xu_hao':0,'jie_dian':[0,0],'E':206000,'A':1,'I':1,'L':1,'a':0}
]


**力输入规范（存储于force.json）**。格式如下：（暂定！！类型代码为两位字符串）  
- xu_hao=0
- wei_zhi=[0]
- lei_xing='00'
- F=1
- a=0
- cos=0
- sin=0
- 均布力特征参数：
- L=1##分布长度，默认为lmm，不与杆件长度关联，属于独立参数
- duan_dian=[0,0]##分别为距离起点和终点的距离，默认整根杆都分布均布力，即距离起点和终点距离都为0
- duan_dian_zhi=[1,1]##线形均布力两边端的值q1和q2
范例：  
[
    {'xu_hao':0,'wei_zhi':[0,0],'lei_xing':'00','L':1,'duan_dian':[10,10],'duan_dian_zhi':[1,1],'F':1,'a':0,'cos':0,'sin':0},
    {'xu_hao':0,'wei_zhi':[0,0],'lei_xing':'00','F':1,'a':0,'cos':0,'sin':0},
    {'xu_hao':0,'wei_zhi':[1,1],'lei_xing':'3','L':100,'duan_dian':[10,10],'duan_dian_zhi':[1,1],'a':0,'cos':0,'sin':0}
]


有关设置的信息，以json格式储存在config文件内，修改、添加设置必须先读取再添加再写入！！
