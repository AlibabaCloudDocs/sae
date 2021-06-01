# 在SAE创建Properties格式的配置后，使用YAML无法访问？

## Condition

在SAE配置中心创建Properties格式的配置后，使用Nacos SDK可以获取，但使用YAML无法访问。

## Cause

Nacos SDK支持解析Properties格式配置，不支持YAML格式。

## Remedy

1.  遇到该问题，需要您自己处理返回值，Nacos SDK无法对返回值格式化。


