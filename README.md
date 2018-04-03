360jiagu
========

容器化360加固Linux版

#### 自适应加固及签名

```bash
docker run -it --rm 
-e USERNAME=username \
-e PASSWORD=password \
-e KEYSTORE_PATH=/output/ririjin.jks \
-e KEYSTORE_PASSWORD=kspassword \
-e ALIAS=rijin \
-e ALIAS_PASSWORD=aliaspassword \
-e OUTPUT=/output \
-e AUTO_SIGN=1 \
-v $PWD:/output idocking/360jiagu:latest jiagu /output/app-release-unsigned.apk
```

#### 原始命令

```bash
docker run -it --rm 
-e USERNAME=username \
-e PASSWORD=password \
-e KEYSTORE_PATH=/output/ririjin.jks \
-e KEYSTORE_PASSWORD=kspassword \
-e ALIAS=rijin \
-e ALIAS_PASSWORD=aliaspassword \
-e CONF_X86="" \
-v $PWD:/output idocking/360jiagu:latest jiagu /output/app-release-unsigned.apk /output -autosign
```

> 不传入`OUTPUT `环境变量，则可以开启原始命令模式, 另外，传入`AUTO_SIGN `无效，请直接在命令中指定，加固后的包下载后是不会自动签名的。


#### 对APK包进行签名

```bash
docker run -it --rm 
-e KEYSTORE_PATH=/output/ririjin.jks \
-e KEYSTORE_PASSWORD=kspassword \
-e ALIAS=rijin \
-e ALIAS_PASSWORD=aliaspassword \
-v $PWD:/output idocking/360jiagu:latest sign /output/app-release-unsigned.apk
```

#### 环境变量说明

名称|描述|情况说明
:--|:--|:--
USERNAME|360加固用户名|如果不传入，则不会执行登录操作，此时请将`jiagu.db`文件映射到`/jiagu/jiagu.db`
PASSWORD|360加固密码|如果不传入，则不会执行登录操作
KEYSTORE_PATH|Keystore路径|如果传入，则会执行`jiagu.jar -importsign`导入秘钥
KEYSTORE_PASSWORD|Keystore密码
AUTO_SIGN|值为1时，加固时会加入参数`-autosign`, 加固后也会自动再次签名
ALIAS|Keystore里的Key的名字
ALIAS_PASSWORD|Keystore里Key的密码
OUTPUT|加固后输出目录|如果此参数为空，则请使用360的 `jiagu.jar -jiagu` 的参数列表
JAR_TIMEOUT|jar执行超时时间，默认为600s|有时候jar会挂掉 
CONF_UPDATE|升级通知|`CONF_UPDATE=0` 为关闭，`CONF_UPDATE=""` 为开启
CONF_CRASHLOG|崩溃日志|`CONF_CRASHLOG=0` 为关闭，`CONF_CRASHLOG=""` 为开启
CONF_X86|x86支持|`CONF_X86=0` 为关闭，`CONF_X86=""` 为开启
CONF_MSG|消息推送|`CONF_MSG=0` 为关闭，`CONF_MSG=""` 为开启
CONF_BUSINESS|商务合作|`CONF_BUSINESS=0` 为关闭，`CONF_BUSINESS=""` 为开启
CONF_NOCERT|跳过签名校验|`CONF_NOCERT=0` 为关闭，`CONF_NOCERT=""` 为开启


