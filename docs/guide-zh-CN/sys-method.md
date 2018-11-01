## 系统常用

目录

- 公用方法
  - 获取单个配置信息
  - 获取全部配置信息
  - 打印调试
  - 行为日志记录
  - 微信接口验证及报错获取
  - 解析 model 报错
  - 变动用户积分/余额接口
- 控制器底层方法
  - 解析 model 报错
- 全局函数
  - 打印调试
- WebHook
  - Gitee 码云

### 公用方法

##### 获取单个配置信息

```
// 注意$fildName 为你的配置标识,默认从缓存读取
Yii::$app->debris->config($fildName);

// 强制不从缓存读取
Yii::$app->debris->config($fildName, true);
```

##### 获取全部配置信息

```
// 注意默认从缓存读取
Yii::$app->debris->configAll();

// 强制不从缓存读取
Yii::$app->debris->configAll(true);
```

##### 打印调试

```
Yii::$app->debris->p();
```

##### 行为日志记录

```
/**
 * 行为日志
 *
 * @param string $behavior 行为标识
 * @param string $remark 备注 注意长度为255
 * @param bool $noRecordData 是否记录 post 数据 [true||false]
 * @throws \yii\base\InvalidConfigException
 */
Yii::$app->debris->log($behavior, $remark, $noRecordData)
```

##### 微信接口验证及报错

验证

```
// 默认直接报错，如果想不直接报错请把true设置为false
Yii::$app->debris->analyWechatPortBack($message, true);
```

报错获取

```
// 注意验证的时候不直接报错才可用
Yii::$app->debris->getWechatPortBackError();
```

##### 解析 model 报错

```
// 注意 $firstErrors 为 $model->getFirstErrors();
Yii::$app->debris->analyErr($firstErrors);
```

##### 变动用户积分/余额接口

```
/**
 * 变动积分
 * 
 * 用户id, 字段名称, 变动数量, 组别(选填), 备注(选填)
 */
\common\models\member\CreditsLog::change(1, 'user_integral', 1, 'sign', '签到增加积分');
```
### 控制器底层方法

##### 解析 model 报错

```
// 注意 $firstErrors 为 $model->getFirstErrors();
$this->analyErr($firstErrors);
```

### 全局函数

##### 打印调试

```
// 注意只能在开发模式下使用，生产模式没有此函数
p($array);
```
  
### WebHook

##### Gitee 码云

1、先到 后台网站设置->WebHook->Gitee 填写好对应的git地址、绝对路径，密码  
2、到 码云项目主页->管理->WebHooks->添加 填写的Post地址为 `http://[你的域名]/api/web-hook/gitee`