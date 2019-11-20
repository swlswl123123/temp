## 数据传输
### 发送方
在从高层接收到PDCP SDU时，发送PDCP实体应启动与此PDCP SDU关联的discardTimer（如果已配置）。     
对于从高层接收到的PDCP SDU，发送PDCP实体应：
1. 将与TX_NEXT对应的COUNT值与此PDCP SDU相关联     
2. 执行PDCP SDU的报头压缩
3. 执行完整性保护
4. 将PDCP数据PDU的PDCP SN设置为TX_NEXT对于$2^{pdcp-SN-SizeUL}$的模值
5. 将TX_NEXT加1
6. 将生成的PDCP数据PDU提交到下面指定的较低层

当向下层提交PDCP PDU时，发送PDCP实体应：   
1. 如果发送PDCP实体与一个RLC实体相关联，则将PDCP PDU提交给相关的RLC实体
2. 如果发送PDCP实体与两个RLC实体相关联：
   - 如果PDCP副本已激活且PDCP PDU是数据PDU，则复制PDCP数据PDU并将PDCP数据PDU提交给两个关联的RLC实体
   - 否则，提交PDCP控制PDU到原始RLC实体
3. 其他情况：
   - 如果两个相关的RLC实体属于不同的小区组