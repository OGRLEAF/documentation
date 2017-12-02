> occ命令是ownCloud/Nextcloud的命令行界面。您可以使用occ执行许多常见的服务器操作，例如安装和升级ownCloud/Nextcloud，管理用户，加密，密码，LDAP设置等。

### OCC命令行工具详解

[ssbluelist]

*   [ownCloud/Nextcloud OCC命令行工具详解（1）](https://www.orgleaf.com/1719.html)
*   [ownCloud/Nextcloud OCC命令行工具详解（2）](https://www.orgleaf.com/2258.html)
*   [ownCloud/Nextcloud OCC命令行工具详解（3）](https://www.orgleaf.com/2502.html)
[/ssbluelist]

## 完整性检查

具有官方标签的插件（Apps）必须是使用拥有Nextcloud签名的代码。没有签名的官方应用程序将无法安装。对第三方插件来说，代码签名（Code Sigining）是可选的。
<pre class="lang:sh decode:true ">integrity
 integrity:check-app                 #检查使用签名的应用程序的完整性。
 integrity:check-core                #检查使用签名的内核的完整性
 integrity:sign-app                  #用私玥为一个app签名
 integrity:sign-core                 #用私玥为核心签名</pre>
创建签名密钥后，以此示例签署您的应用：
<pre class="lang:sh decode:true ">sudo -u www-data php occ integrity:sign-app --privateKey=/Users/lukasreschke/contacts.key --certificate=/Users/lukasreschke/CA/contacts.crt --path=/Users/lukasreschke/Programming/contacts</pre>
验证你的应用：
<pre class="lang:sh decode:true ">sudo -u www-data php occ integrity:check-app --path=/pathto/app appname</pre>
如果你的应用的签名是正确的，那么就不会输出任何信息。如果返回了错误信息，可以参考开发者文档中的[Code Signing](https://docs.nextcloud.org/server/11/developer_manual/app/code_signing.html#how-to-get-your-app-signed) 获取详细信息。发布应用时要做的: 更新版本号。
<pre class="lang:default decode:1 inline:1 ">integrity:sign-core</pre>
仅供Nextcloud核心开发人员使用。

了解更多：[_Code Signing_](https://docs.nextcloud.com/server/11/admin_manual/issues/code_signing.html)

## LDAP命令

[infobox]LDAP命令只在“LDAP user and group backend” 应用激活后才能使用[/infobox]

只有当您启用了LDAP应用程序时，才会显示这些LDAP命令。
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true">ldap
 ldap:check-user               #检查一个用户是否存在于LDAP中
 ldap:create-empty-config      #创建一个空的LDAP配置
 ldap:delete-config            #删除一个LDAP配置
 ldap:search                   #搜索用户或者组
 ldap:set-config               #修改LDAP配置
 ldap:show-config              #显示LDAP设置
 ldap:show-remnants            #显示那些用户在LDAP上没有信息，但是在Nextcloud中仍然存在
 ldap:test-config              #测试LDAP配置</pre>
使用以下语法搜索LDAP用户：
<pre class="lang:default decode:true">sudo -u www-data php occ ldap:search [--group] [--offset="..."]
[--limit="..."] search</pre>
搜索结果从关键词的开头开始匹配，可以看下面搜索关键词“rob”的例子：
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="搜索规则">sudo -u www-data php occ ldap:search "rob"</pre>
这样会搜索到所有以“rob”开头的词，例如<span style="background-color: #00ffff;">rob</span>bie、<span style="background-color: #00ffff;">rob</span>erta或<span style="background-color: #00ffff;">rob</span>in。如果要搜索所有包含“rob”的词，可以使用通配符：
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="使用通配符搜索">sudo -u www-data php occ ldap:search "*rob"</pre>
用户搜索属性可以用
<pre class="lang:default decode:1 inline:1 ">ldap:set-config</pre>
来设置搜索属性。例如，如果将属性设置为
<pre class="lang:default decode:1 inline:1 ">givenName</pre>
和
<pre class="lang:default decode:1 inline:1 ">sn</pre>
，你就可以用姓+名的方式快速搜索。比如：用省略的字母
<pre class="lang:default decode:1 inline:1 ">te ha</pre>
来代替全名
<pre class="lang:default decode:1 inline:1 ">Terri Hanson</pre>
进行搜索。后面跟着的空格将会被省略。

检查一个LDAP用户是否存在。（只能在Nextcloud连接LDAP服务器后使用）
<pre class="lang:sh decode:true " title="检查LDAP用户">sudo -u www-data php occ ldap:check-user robert</pre>
当发现有的LDAP连接被禁用时，
<pre class="lang:default decode:1 inline:1 ">ldap:check-user</pre>
不会运行，这是为了防止由于无法在禁用的LDAP服务器上查找该用户而误将这个用户标记为“不存在”。如果你确定所查找的用户不在已禁用的LDAP连接上，可以使用
<pre class="lang:default decode:1 inline:1 ">-force</pre>
强制在所有未禁用的连接上执行搜索：
<pre class="lang:sh decode:true " title="强制搜索">sudo -u www-data php occ ldap:check-user --force robert</pre>
<pre class="lang:default decode:1 inline:1 ">ldap:create-empty-config</pre>
会创建一个空的LDAP配置。所创建的第一个配置是没有
<pre class="lang:default decode:1 inline:1 ">configID</pre>
的，就像下面这样：
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true">sudo -u www-data php occ ldap:create-empty-config
  Created new configuration with configID ''</pre>
在没有创建其它配置的情况下，所创建的第二个配置及之后所创建的配置会自动分配ID：
<pre class="lang:default decode:true ">sudo -u www-data php occ ldap:create-empty-config
   Created new configuration with configID 's01'</pre>
接下来你可以列出你所有的配置：
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="列出配置">sudo -u www-data php occ ldap:show-config</pre>
然后根据配置的ID来查看某一个配置:
<pre class="lang:sh decode:true " title="查看配置">sudo -u www-data php occ ldap:show-config s01</pre>
<pre class="lang:default decode:1 inline:1 ">ldap:delete-config [configID]</pre>
可以用来删除一个存在的配置：
<pre class="lang:sh decode:true " title="删除配置">sudo -u www-data php occ ldap:delete s01
Deleted configuration with configID 's01'</pre>
<pre class="lang:default decode:1 inline:1 ">ldap:set-config</pre>
用于操作配置，例如之前提到的设置搜索属性：
<pre class="lang:sh decode:true " title="设置搜索属性">sudo -u www-data php occ ldap:set-config s01 ldapAttributesForUserSearch
"cn;givenname;sn;displayname;mail"</pre>
<pre class="lang:default decode:1 inline:1 ">ldap:test-config</pre>
用于测试你的配置是否有效和能否应用到服务器上：
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="测试配置">sudo -u www-data php occ ldap:test-config s01
The configuration is valid and the connection could be established!
#配置有效，可以建立连接！</pre>
<pre class="lang:default decode:1 inline:1 ">ldap:show-remnants</pre>
可以用于清理LDAP映射表，具体可查看文档 [_LDAP User Cleanup_](https://docs.nextcloud.com/server/12/admin_manual/configuration_user/user_auth_ldap_cleanup.html)。

## 日志命令

以下命令可用于查看或配置记录日志的首选项：
<pre class="lang:sh decode:true " title="日志命令">log
 log:manage     #管理日志配置
 log:owncloud   #操作Nextcloud日志后端</pre>
运行
<pre class="lang:default decode:1 inline:1 ">log:owncloud</pre>
可以查看你当前的日志状态：
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="查看日志状态">sudo -u www-data php occ log:owncloud
Log backend Nextcloud: enabled                   #Nextcloud后台日志：启用
Log file: /opt/nextcloud/data/nextcloud.log      #日志存放位置
Rotate at: disabled                              #日志轮转：禁用</pre>
使用
<pre class="lang:default decode:1 inline:1 ">--enable</pre>
来启用日志。使用
<pre class="lang:default decode:1 inline:1 ">--file</pre>
来修改日志存放位置。使用
<pre class="lang:default decode:1 inline:1 ">--rotate-size</pre>
设置日志轮转的文件大小，0 则为禁用日志轮转。
<pre class="lang:default decode:1 inline:1 ">log:manage</pre>
设置你的日志后端、日志级别和时区，默认的配置分别是
<pre class="lang:default decode:1 inline:1 ">owncloud</pre>
.
<pre class="lang:default decode:1 inline:1 ">Warning</pre>
,和
<pre class="lang:default decode:1 inline:1 ">UTC</pre>
，可选的配置有

[ssbluelist]

*   –backend [owncloud, syslog, errorlog]
*   –level [debug, info, warning, error]
[/ssbluelist]

## 维护模式命令

当你升级Nextcloud、配置加密、执行备份或者其它需要暂时禁止用户使用的任务时，可以使用下面的命令配置维护模式：
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="维护模式">maintenance
 maintenance:data-fingerprint        #备份恢复后更新系统数据指纹
 maintenance:mimetype:update-db      #更新数据库mimetype并刷新文件缓存
 maintenance:mimetype:update-js      #更新mimetypelist.js
 maintenance:mode                    #启用维护模式
 maintenance:repair                  #修复安装
 maintenance:update:htaccess         #更新.htaccess文件</pre>
<pre class="lang:default decode:1 inline:1 ">maintenance:mode</pre>
会锁定所有已登录的用户（包括管理员），并显示一个状态页面来提示服务器处于维护模式，未登录的用户将暂时无法登录，直到维护模式关闭。在服务器退出维护模式之后，已登录的用户必须要刷新浏览器页面后才能继续使用。
<pre class="lang:sh decode:true " title="维护模式的启用和关闭">sudo -u www-data php occ maintenance:mode --on
sudo -u www-data php occ maintenance:mode --off</pre>
在重置数据备份或数据库备份后，应当先使用
<pre class="lang:default decode:1 inline:1 ">maintenance:data-fingerprint</pre>
。这会改变所有文件在与同步客户端通信所用的ETag(被请求变量的实体值)，使客户端意识到文件已经被改变。
<pre class="lang:default decode:1 inline:1 ">maintenance:repair</pre>
会在升级过程中自动运行以清理数据库，所以往往不需要特意运行它：
<pre class="lang:sh decode:true " title="清理命令">sudo -u www-data php occ maintenance:repair</pre>
<pre class="lang:default decode:1 inline:1 ">maintenance:mimetype:update-db</pre>
可以根据 `<span class="pre">config/mimetypemapping.json</span>`来识别更改了mime类型的文件，并更新数据库和文件缓存。这个命令往往在修改`<span class="pre">config/mimetypemapping.json</span>`后使用。如果你动了mime类型，可以运行
<pre class="lang:default decode:1 inline:1 ">maintenance:mimetype:update-db --repair-filecache</pre>
来将更改应用到存在的文件。

## 安全

使用这些命令来管理服务器范围的SSL证书。当您使用自签名证书的其他Nextcloud服务器创建联合共享时，这些功能很有用：
<pre class="lang:default decode:true " title="安全命令">security
 security:certificates         list trusted certificates
 security:certificates:import  import trusted certificate
 security:certificates:remove  remove trusted certificate</pre>
列出所有已安装的证书：
<pre class="lang:default decode:true">sudo -u www-data php occ security:certificates</pre>
导入一个新的证书：
<pre class="lang:default decode:true ">sudo -u www-data php occ security:import /path/to/certificate</pre>
移除一个证书：
<pre class="lang:default decode:true ">sudo -u www-data php occ security:remove [证书的文件名]</pre>

## 垃圾桶（回收站）

[infobox]这个命令只在插件（应用）file_trashbin启用时可用。启用插件（应用）后，用户删除的文件将不会在服务器上立即删除[/infobox]
<pre class="lang:default decode:1 inline:1 ">trashbin:cleanup</pre>
用于移除特定用户已删除的文件，多个用户名使用空格隔开。如果没有指定用户，则删除所有用户已删除的文件。
<pre class="lang:default decode:true " title="垃圾箱">trashbin
 trashbin:cleanup   移除已删除的文件</pre>
下面是一个清理所有用户已删除的文件的例子：
<pre class="lang:default decode:true " title="清理用户文件">sudo -u www-data php occ trashbin:cleanup
Remove all deleted files
Remove deleted files for users on backend Database
 freda
 molly
 stash
 rosa
 edward</pre>
下面是一个清理特定用户molly和freda的已删除文件的例子：
<pre class="lang:default decode:true " title="清理特定用户文件">sudo -u www-data php occ trashbin:cleanup molly freda
Remove deleted files of   molly
Remove deleted files of   freda</pre>

### 用户管理命令

用户管理命令
<pre class="lang:default decode:1 inline:1 ">user</pre>
用于创建和删除用户、重置密码、显示一个简单的关于你有多少用户以及用户最后登录时间的报告：
<pre class="lang:default decode:true " title="用户管理命令">user
 user:add                            #添加用户
 user:delete                         #删除特定的用户
 user:disable                        #禁用特定的用户
 user:enable                         #激活特定的名号
 user:lastseen                       #显示用户最后登录的时间
 user:report                         #显示已有多少用户访问
 user:resetpassword                  #为用户重置密码
 user:setting                        #阅读或修改用户设置</pre>
你可以用`<span class="pre">display-name</span>` 、登录名和组用户关系来添加一个用户，语法为：
<pre class="lang:default decode:true " title="添加用户">user:add [--password-from-env] [--display-name[="..."]] [-g|--group[="..."]]
uid</pre>
`<span class="pre">display-name</span>` 是指在浏览器中用户页面上的全名，uid是指用户的**Username**，即用户登录所用的账号名。例如添加一个名为Layla Smith的新用户，并将她添加至**users**和**db-admins**组，如果组不存在的话就会自动创建：
<pre class="lang:default decode:true " title="创建新用户示例">sudo -u www-data php occ user:add --display-name="Layla Smith"
  --group="users" --group="db-admins" layla
  Enter password:
  Confirm password:
  The user "layla" was created successfully
  Display name set to "Layla Smith"
  User "layla" added to group "users"
  User "layla" added to group "db-admins"</pre>
前往用户页面，你就会看到刚添加的新用户。
<pre class="lang:default decode:1 inline:1 ">password-from-env</pre>
允许您从环境变量中设置用户密码。这样可以防止密码通过进程列表暴露给所有用户，并且只能在运行该命令的用户（root）的历史记录中显示。这也允许创建添加多个新用户的脚本。
<pre class="lang:default decode:1 inline:1 ">password-from-env</pre>
要求在root账户下运行，而不是使用sudo来获取root权限。因为sudo剥离环境变量。下面是一个添加名为Fred的新用户的示例：
<pre class="lang:default decode:true" title="使境变量创建用户">export OC_PASS=新密码
su -s /bin/sh www-data -c 'php occ user:add --password-from-env
  --display-name="Fred Jones" --group="users" fred'
The user "fred" was created successfully
Display name set to "Fred Jones"
User "fred" added to group "users"</pre>
你可以重置用户的密码，包括管理员的密码，详细内容可参考：[ownCloud/Nextcloud使用OCC命令重置密码](https://www.orgleaf.com/2147.html)
<pre class="lang:default decode:true" title="为用户重置密码">sudo -u www-data php occ user:resetpassword layla
  Enter a new password:
  Confirm the new password:
  Successfully reset password for layla
</pre>
你也可以使用
<pre class="lang:default decode:1 inline:1 ">password-from-env</pre>
来重置用户密码：
<pre class="lang:default decode:true" title="使用环境变量设置密码">export OC_PASS=新密码
su -s /bin/sh www-data -c 'php occ user:resetpassword --password-from-env
layla'
Successfully reset password for layla</pre>
删除用户：
<pre class="lang:default decode:true " title="删除用户">sudo -u www-data php occ user:delete fred</pre>
查看用户最近的登录：
<pre class="lang:default decode:true " title="查看用户最近登录">sudo -u www-data php occ user:lastseen layla
  layla's last login: 09.01.2015 18:46</pre>
读取用户的配置：
<pre class="lang:default decode:true " title="读取用户设置">sudo -u www-data php occ user:setting layla
  - core:
    - lang: en
  - login:
    - lastLogin: 1465910968
  - settings:
    - email: layla@example.tld</pre>
按插件（应用）筛选配置：
<pre class="lang:default decode:true " title="按应用筛选">sudo -u www-data php occ user:setting layla core
- core:
- lang: en</pre>
单独获取某一项配置：
<pre class="lang:default decode:true " title="单独获取某项设置">sudo -u www-data php occ user:setting layla core lang
en</pre>
修改用户配置 :(  ：
<pre class="lang:default decode:true " title="设置">sudo -u www-data php occ user:setting layla settings email "new-layla@example.tld"</pre>
删除某一项配置：
<pre class="lang:default decode:true" title="删除用户某项配置">sudo -u www-data php occ user:setting layla settings email --delete</pre>
生成一个统计所有用户的简单的报告，包括外部验证用户（例如LDAP）：
<pre class="lang:default decode:true" title="生成用户统计报告">sudo -u www-data php occ user:report
+------------------+----+
| User Report      |    |
+------------------+----+
| Database         | 12 |
| LDAP             | 86 |
|                  |    |
| total users      | 98 |
|                  |    |
| user directories | 2  |
+------------------+----+</pre>

## 版本控制

[infobox]这组命令只有在版本控制插件（应用）启用时可用[/infobox]

使用此命令删除特定用户的文件版本，或者在没有指定的情况下为所有用户删除文件版本：
<pre class="lang:default decode:true " title="删除版本">versions
 versions:cleanup   #删除版本</pre>
这是一个删除所有用户的版本的例子：
<pre class="lang:default decode:true " title="删除所有用户的版本">sudo -u www-data php occ versions:cleanup
Delete all versions
Delete versions for users on backend Database
  freda
  molly
  stash
  rosa
  edward</pre>
你可以为特定用户删除版本，多个用户使用空格隔开
<pre class="lang:default decode:true" title="删除特定用户版本">sudo -u www-data php occ versions:cleanup freda molly
Delete versions of   freda
Delete versions of   molly</pre>

## 使用命令行工具安装Nextcloud

[使用命令行安装Nextcloud](https://www.orgleaf.com/2728.html)

* * *

OCC命令行工具到此翻译完毕。欢迎纠错！

[![](https://img.orgleaf.com/2017/02/slider1-occ.png)](https://img.orgleaf.com/2017/02/slider1-occ.png)
