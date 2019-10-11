# greatwa11

- 在Aliyun海外region比如（东南亚）购买ECS
  - 参考配置
    - `1` CPU + `0.5`GB内存按量付费ECS, 比如 `ecs.t5-lc2m1.nano` 规格
    - `50MB`按使用流量付费带宽
    - Ubuntu 16.04 64位
    - 需要`公网IP`
- ssh登录ECS install `pip` & `shadowsocks`
    ```
            apt update
            apt install python-pip
            pip install shadowsocks
    ```
- 配置shadowsocks

    ```
            vim /etc/ss.json
    ```
    填入如下内容, 密码根据自己情况实际填写
    ```
    {
        "server": "0.0.0.0",
        "server_port": 4500,
        "password": "<input your password here>",
        "method": "aes-256-cfb"
    }
    ```
- start shadowsocks service
    ```
        ssserver -c /etc/ss.json -d start
    ```

- 在ECS安全组打开4500端口的TCP入网权限
    ```
    规则方向：  入方向
    授权策略：  允许
    协议类型：  自定义TCP
    端口范围：  4500/4500
    授权类型：  IPv4地址段访问
    授权对象：  0.0.0.0/0
    ```

- 连接
    - Android App(Shadowsocks/影梭)
    - IOS App (Wingy)
    
    ```
    服务器地址就是ECS的公网IP
    远程端口 4500（如果改了端口这里对应就行，不一定是4500）
    密码就是配置文件中填写的password
    加密方式选择 AES-256-CFB
    ```
