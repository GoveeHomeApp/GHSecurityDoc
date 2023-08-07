# GHSecurityDoc
当前仓库是对app安全探索与整理的合集<br>

## Step1：简要划分
1.代码层面<br>
数据加密：重要的数据或者字符硬编码，以加密或者特殊代码的形式呈现。<br>
代码混淆：将代码混淆成比较难懂逻辑，打乱代码顺序，增加攻击者的理解难度。<br>
（以上两种均可通过加固工具实现）<br>
2.外部层面<br>
各种来自外部的App安全威胁（例如：越狱设备，debugger 模拟器调试）<br>
代码中检测获取、代码外部防护<br>
3.网络层面<br>
防抓包：通过SeverTrust证书配置，防止网络抓包这种中间人行为，以防请求报文被篡改。<br>
服务端也要通过网关层或者相应的Auth机制去限制。<br>
4.逆向层面<br>
防调试：防止动态调试、防注入、防hook。<br>
防反编译：防止App被逆向工具获取Mach-O具体信息，以获取对应段信息。<br>
5.其他方向<br>
蓝牙安全相关（待定）<br>
保持你的操作系统版本更新 不使用越狱设备（）提到的最多。<br>

## Step2：相关介绍

#### 关于代码混淆
1.字符串加密<br>
2.代码逻辑混淆<br>
（Swift 有一个swiftshield，当然也可以选择付费的加密混淆工具，很多厂商都有提供；如果自己做，那就是需要自己去找分别对应的库去弄）<br>

``` shell
    @usableFromInline class G__ee1pd4a {
    @usableFromInline static let a: String = {
      var a: [UInt8] = [124, 40, 121, 121, 125, 127, 44, 126, 45, 44, 121, 122, 44, 121, 120, 44, 127, 126, 47, 121, 122, 127, 112, 127, 45, 121, 126, 40, 121, 124, 113, 45, 124, 40, 122, 127, 120, 44, 125, 127, 120, 45, 121, 40, 125, 123, 125, 122, 40, 113, 113, 125, 113, 127, 45, 113, 122, 47, 123, 40, 120, 123, 121, 45]
      for i in 0 ..< 64 {
        a[i] ^= 73
      }
      return String(bytes: a, encoding: .utf8)!
    }()
    }
```

#### 代码层面一些安全检查
1.debug环境检查（主要是操控与查看ptrace）<br>
2.模拟器运行检查（很简单）<br>
3.文件检查（包含所有卷宗路径、访问权限、可疑名称、伪装文件等、文件完整性校验）<br>
4.fishHook、 或者其他常见Hook类型检查 <br>
5.越狱检测（外链App开启、private路径下可疑文件或者可疑文件权限检查等）<br>
6.网络代理（proxy）检测 <br>
7.逆向工程检查（包含可疑文件、DYLD、openPorts、pSelectFlag）<br>
8.Runtime HOOK checker <br>

#### 有关App请求
1.HTTPS（Alamofire证书配置相关）、身份校验防抓包（防中间人劫持）<br>

#### 有关逆向工程与反编译
逆向与反编译这块 需要越狱设备以及Mach-O View、Hooper、idapro等软件支持 细节放在务虚或者二期去深入<br>

#### 有关蓝牙的安全
及时更新操作系统针对蓝牙漏洞的补丁
[相关链接](https://us.norton.com/blog/mobile/bluetooth-security)https://us.norton.com/blog/mobile/bluetooth-security

后续会有继续更新 敬请期待 <br>

如果有相关方向的想法和建议 欢迎讨论交流 <br>

