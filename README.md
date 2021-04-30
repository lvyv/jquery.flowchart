
物联网配置前端
================

本项目利用Javascript jQuery plugin来配置物联网通道。[请看实例](https://lvyv.github.io/jquery.flowchart/demo/demo.html)。


待办事项
-----------

 - [ ] 需要解决Operator类型逻辑关系；
 - [ ] 需设计属性页，每个Operator和link可以通过属性页进行编辑；
 - [ ] 改造node exporter，完成配置文件下发。

DAG技术方案
-------
本期DAG设计范围限定：
- 设计涵盖4类通信节点，CLI，SVR_HTTP，SVR_MQTT，UDP和1类万能节点。前面4种节点是用于表示开发完成的成熟软件。万能节点是用于表示用户可编程的调测数据生成节点。
- 设计涵盖两类边，配置关系边和数据调测边。配置关系边表示成熟软件的配置软件指向关系。数据调测边表示临时生成数据如何发送到成熟节点。

对于这四类节点，CLI是用户定制的，其它节点都是写好的。
它们之间连接约束关系如下表。
||CLI|SVR_MQTT|SVR_HTTP|UDP
|--|--|--|--|--
|CLI|-|Y|Y|Y
|SVR_MQTT|Y|--|--|--
|SVR_HTTP|Y|--|--|--
|UDP|Y|--|--|Y

**`CLI/SVR(HTTP)`**
|TCP HTTP| ||
|--|--|--|
|| SVR_WEST|SVR_EAST|
|CLI_OUT|POST |-|
|CLI_IN|-|GET|

**`CLI/SVR(MQTT)`**
|TCP MQTT| ||
|--|--|--|
|| SVR_WEST|SVR_EAST|
|CLI_OUT|PUB |-|
|CLI_IN|-|SUB|

**`P2P/SVR(UDP)`**
|UDP P2P| ||
|--|--|--|
|| SVR_WEST|SVR_EAST|
|CLI_OUT|SEND_TO|-|
|CLI_IN|-|RECV_FROM|


![系统总体架构](https://lvyv.github.io/jquery.flowchart/images/architecture-ovw.svg)

许可协议
-------
jquery.flowchart.js is under [MIT license](https://github.com/sdrdis/jquery.flowchart/blob/master/MIT-LICENSE.txt).

作者
-------
* [吕昱](https://github.com/lvyv) 

贡献者
------------
本项目来自[Sebastien Drouyer](http://sebastien.drouyer.com/)的工作。

