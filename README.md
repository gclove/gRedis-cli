# gRedis-cli

## 介绍
这是一个使用golang开发的redis交互式命令行，希望能解决一些redis原生cli使用中的痛点。项目处于起步阶段，功能并不完全。

[项目地址](https://github.com/dalebao/gRedis-cli)

## 出发点：
1. 在工作中，会生成很多规律的redis键，如：test_1,test_2，当需要人肉删除test_*键的时候，使用原生redis-cli，痛苦。
2. 在工作中，redis键太多，常常会让人忘记redis键的类型，需要先type再用对应类型的查询命令查询，太累。

## 特点：
1. 使用一个命令，查询string,hash,list,set,zset类型的数据
2. 批量查询redis键的ttl
3. 批量查询redis键的类型
4. 使用通配符匹配redis键，选择或直接删除redis键
5. 使用table直观展示redis操作情况

![e](https://github.com/dalebao/gRedis-cli/raw/master/v1Show.png)

## 命令与使用：
```
git clone https://github.com/dalebao/gRedis-cli.git
cd gRedis-cli
go run main.go
```
按照流程填写服务器连接信息

### get
   查询string,hash,list,set,zset类型的数据
    `get redisKey`
    
    
### keys
   使用通配符匹配redis键，返回redis键与对应类型
   
    `keys *`
    
   #### 辅助命令
  `keys * -only=string,hash limit=10 sort=asc`
  
   1. only=string,hash 仅展示 string 和 hash 类型键,多种类型用 *,* 分割
   
   2. expect=string,hash 排除展示 string 和 hash 类型键,多种类型用 *,* 分割
   
   3. limit=10 控制展示数据数量，取N条数据展示
   
   4. sort=asc 按照键类型名称的升降序排序展示数据 
   
   5. export=csv 将结果导出成csv文件 目前支持类型 `csv`
    
### type
   批量查询redis键类型
    `type redisKey1 redisKey2`
    
### ttl
   批量查询redis ttl信息
    `ttl redisKey1 redisKey2`
    
### expire
   设置redis键过期时间
   `expire redisKey1 100` 单位秒
   
### del
   批量删除redis键
   `del redisKey1 redisKey2`

### rdel
   匹配redis键，直接或选择删除redis键
   `rdel redis*`
   
### 退出
   输入 `quit`
   
## 接下来要做
1. 继续完善查询功能
2. 考虑是否要增加修改redis键内容
3. 增加配置保存功能，避免重复输入配置信息
4. 思考大量数据redis键的处理方式
5. 期待在issue中与我交流
   
## 鸣谢
[命令行构建工具](https://github.com/AlecAivazis/survey)

[golang表格构建工具](https://github.com/modood/table)
    
    