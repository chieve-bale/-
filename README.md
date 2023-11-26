结构力学求解器cumt
##单位统一为：长度mm，力N，应力MPa，默认E=206000MPa ，角度默认 °（逆时针为正）

力的类型有待商榷
#力的类型暂定为
  0：节点力
  1：节间力
    0：轴向力
    1：集中竖向力
    2：斜向力
    3：集中剪力
    4：集中弯矩
  5：均布力，需要补充长度（分数表示）、均布力的局部坐标系下的函数表达式{'a':0,'sin':0,'cos':0,'b':0}。此局部坐标系x轴与整体坐标系的x轴指向近似。

##杆件索引使用杆件的编码不使用节点编码！！！

##中间过程的数据交换尽量使用json，并确认（ensure_ascii=False, encoding='utf-8'）这两项参数以保证中文的正确显示可可读性。
***
计算程序读取杆件gan_jian_lib.json。序号、节点(类型为元组)为必须参数，杆件角度或三角函数值二选一。格式如下：

[
    {'xu_hao':0,'jie_dian':[0,1],'E':206000,'A':1,'I':1,'L':1,'a':0,'cos':0,'sin':0},
    {'xu_hao':1,'jie_dian':[1,2],'E':206000,'A':1,'I':1,'L':1,'a':0,'cos':0,'sin':0},
    {'xu_hao':2,'jie_dian':[3,7],'E':206000,'A':1,'I':1,'L':1,'a':0,'cos':0,'sin':0},
    {'xu_hao':3,'jie_dian':[3,4],'A':1,'I':1,'L':1,'a':0,'cos':0,'sin':0},
    {'xu_hao':4,'jie_dian':[5,7],'E':206000,'I':1,'L':1,'a':0,'cos':0,'sin':0},
    {'xu_hao':0,'jie_dian':[0,0],'E':206000,'A':1,'L':1,'a':0,'cos':0,'sin':0},
    {'xu_hao':0,'jie_dian':[0,0],'E':206000,'A':1,'I':1,'a':0,'cos':0,'sin':0},
    {'xu_hao':0,'jie_dian':[0,0],'E':206000,'A':1,'I':1,'L':1,'cos':0,'sin':0},
    {'xu_hao':0,'jie_dian':[0,0],'E':206000,'A':1,'I':1,'L':1,'a':0},
]
***
计算程序读取力的json文件为force.json。格式如下：（暂定！！类型代码为两位字符串）
[
    {'xu_hao':0,'wei_zhi':[0,0],'lei_xin':'00','chang_du':1,'han_shu':{'a':0,'sin':0,'cos':0,'b':0},'F':1,'a':0,'cos':0,'sin':0}


]
