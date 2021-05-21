# 调用API次数过多导致限流，怎么处理？

## Condition

调用API时次数过多，提示“Failed to get change order info：Throttling.User：Request was denied due to user flow control .RequestID:XXXXXXXXX”。

## Cause

当前的限流阈值为单用户一分钟60次API调用， 同时调用多个API时容易被限流。

## Remedy

1.  -   [提交工单](https://workorder.console.aliyun.com/)
-   扫描下面的二维码或搜索钉钉群号23198618，在钉钉群联系技术支持。
![SAE钉钉群2](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1176199061/p72048.png)


