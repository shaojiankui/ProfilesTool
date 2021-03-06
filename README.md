# ProfilesManager
iOS Provisioning Profiles, .mobileprovision files manager tool for mac

## Features
### 2.4
- Right-click Item Beautify Filename 右键美化物理文件名，通过双击安装的描述文件名都是UUID，美化过后与AppStore描述文件名一致。
 
### 2.3
- onekey uninstall or install quicklook plug-in,support view the .ipa/.xcarchive/.appex/.mobileprovision/.provisionprofile files directly use the the blank space key.   点击左上角的快速预览按钮，安装插件。插件可以直接预览后缀为.ipa/.xcarchive/.appex/.mobileprovision/.provisionprofile的文件,在文件上空格即可.

### 2.2
- click header sort 点击头部排序
- multi-select opration such show in finder and delete 多选操作，例如在访达中显示和删除
- click reset button，reset window frame and position 点击重置按钮重置window大小与位置

### 1.1
- simple full text search filter 全文搜索后过滤描述文件

### 1.0
- tree look all profiles 树形查看电脑中所有描述文件
- Right-click DeveloperCertificates field item export cer from profile 右键DeveloperCertificates字段里的内容从描述文件中导出cer证书文件
- Right-click Item move to trash  右键移动到废纸篓
- Right-click Item show in finder  右键在finder中显示
- drag muti files install   拖拽描述文件文件直接安装
- Right-click Item export profile 右键导出描述文件
- drag into and look ipa profile or plist directly 拖入ipa快速查看描述文件与info.plist信息




## Download APP
https://github.com/shaojiankui/ProfilesManager/releases

## Screenshot
![](https://raw.githubusercontent.com/shaojiankui/ProfilesManager/master/demo.jpg)

## Provisioning Profile 的构成
以下为典型供应配置文件*.mobileprovision的构成简析：

1. Name：该mobileprovision的文件名。
2. UUID：该mobileprovision文件的真实文件名。
3. TeamName：Apple ID账号名。
4. TeamIdentifier：Team Identity。
5. AppIDName：explicit/wildcard App ID name（ApplicationIdentifierPrefix）。
6. ApplicationIdentifierPrefix：完整App ID的前缀（TeamIdentifier.*）。
7. DeveloperCertificates：包含了可以为使用该配置文件应用签名的所有证书<data><array>。
> 证书是基于Base64编码，符合PEM(PrivacyEnhanced Mail, RFC 1848)格式的，可使用OpenSSL来处理（opensslx509 -text -in file.pem）。
> 
> 从DeveloperCertificates提取<data></data>之间的内容到文件cert.cer（cert.perm）：
> 
> -----BEGIN CERTIFICATE-----
> 
> 将<data></data>之间的内容拷贝至此
> 
> -----END CERTIFICATE-----
> 
> Mac下右键QuickLook 查看cert.cer（cert.perm），在Keychain Access中右键Get Info查看对应证书ios_development.cer，正常情况（公私钥KeyPair配对）应吻合；Windows下没有足够信息 （WWDRCA.cer），无法验证该证书。
> 
> 如果你用了一个不在这个列表中的证书进行签名，无论这个证书是否有效，这个应用都将CodeSign Fail。

8. Entitlements键<key>对应的<dict>：
> **keychain-access-groups**：$(AppIdentifierPrefix)，参见Code Signing Entitlements(*.entitlements)。
> 
> 每个应用程序都有一个可以用于安全保存一些如密码、认证等信息的keychain，一般而言自己的程序只能访问自己的keychain。通过对应用签名时的一些设置，还可以利用keychain的方式实现同一开发者签证（就是相同bundle seed）下的不同应用之间共享信息的操作。比如你有一个开发者帐户，并开发了两个不同的应用A和B，然后通过对A和B的keychain access group这个东西指定共用的访问分组，就可以实现共享此keychain中的内容。
> 
> **application-identifier**：带前缀的全名，例如$(AppIdentifierPrefix)com.apple.garageband。
> 
> **com.apple.security.application-groups**：App Group ID（group. com.apple），参见Code Signing Entitlements(*.entitlements)。
> 
> **com.apple.developer.team-identifier**：同Team Identifier。

9. ProvisionedDevices：该mobileprovision授权的开发设备的UDID <array>。
> Provisioning Profile被配置到【XcodeTarget|Build Settings|Code Signing|Provisioning Profile】下，然后在Code Signing Identity下拉可选择Identities from Profile "..."（即Provisioning Profile中包含的Certificates）。


## License

ProfilesManager is available under the MIT license.
