## 使用OCC命令

OCC文件是使用PHP编写的，首先你要找到OCC文件在哪里

它在ownCloud/Nextcloud根目录里，比如/var/www/html/owncloud/OCC，请确认OCC文件的用户和组均为网页服务器用户，且用户和组权限可读可执行

Ubuntu/Debian用户可以直接在ownCloud/Nextcloud根目录下执行：
<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true">sudo -u www-data php occ #以www-data用户身份执行OCC文件</pre>
会输出以下内容（以Nextcloud为例）：
<pre class="height-set:true height:350 lang:sh decode:true">Nextcloud version 11.0.1

Usage:
  command [options] [arguments]

Options:
  -h, --help            Display this help message
  -q, --quiet           Do not output any message
  -V, --version         Display this application version
      --ansi            Force ANSI output
      --no-ansi         Disable ANSI output
  -n, --no-interaction  Do not ask any interactive question
      --no-warnings     Skip global warnings, show command output only
  -v|vv|vvv, --verbose  Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug

Available commands:
  _completion                         BASH completion hook.
  check                               check dependencies of the server environment
  help                                Displays help for a command
  list                                Lists commands
  status                              show some status information
  upgrade                             run upgrade routines after installation of a new release. The release has to be installed before.
 app
  app:check-code                      check code to be compliant
  app:disable                         disable an app
  app:enable                          enable an app
  app:getpath                         Get an absolute path to the app directory
  app:list                            List all available apps
 background
  background:ajax                     Use ajax to run background jobs
  background:cron                     Use cron to run background jobs
  background:webcron                  Use webcron to run background jobs
 config
  config:app:delete                   Delete an app config value
  config:app:get                      Get an app config value
  config:app:set                      Set an app config value
  config:import                       Import a list of configs
  config:list                         List all configs
  config:system:delete                Delete a system config value
  config:system:get                   Get a system config value
  config:system:set                   Set a system config value
 dav
  dav:create-addressbook              Create a dav addressbook
  dav:create-calendar                 Create a dav calendar
  dav:sync-birthday-calendar          Synchronizes the birthday calendar
  dav:sync-system-addressbook         Synchronizes users to the system addressbook
 db
  db:convert-type                     Convert the Nextcloud database to the newly configured one
  db:generate-change-script           generates the change script from the current connected db to db_structure.xml
 encryption
  encryption:change-key-storage-root  Change key storage root
  encryption:decrypt-all              Disable server-side encryption and decrypt all files
  encryption:disable                  Disable encryption
  encryption:enable                   Enable encryption
  encryption:encrypt-all              Encrypt all files for all users
  encryption:list-modules             List all available encryption modules
  encryption:set-default-module       Set the encryption default module
  encryption:show-key-storage-root    Show current key storage root
  encryption:status                   Lists the current status of encryption
 federation
  federation:sync-addressbooks        Synchronizes addressbooks of all federated clouds
 files
  files:cleanup                       cleanup filecache
  files:scan                          rescan filesystem
  files:transfer-ownership            All files and folders are moved to another user - shares are moved as well.
 files_external
  files_external:applicable           Manage applicable users and groups for a mount
  files_external:backends             Show available authentication and storage backends
  files_external:config               Manage backend configuration for a mount
  files_external:create               Create a new mount configuration
  files_external:delete               Delete an external mount
  files_external:export               Export mount configurations
  files_external:import               Import mount configurations
  files_external:list                 List configured admin or personal mounts
  files_external:notify               Listen for active update notifications for a configured external mount
  files_external:option               Manage mount options for a mount
  files_external:verify               Verify mount configuration
 group
  group:adduser                       add a user to a group
  group:list                          list configured groups
  group:removeuser                    remove a user from a group
 integrity
  integrity:check-app                 Check integrity of an app using a signature.
  integrity:check-core                Check integrity of core code using a signature.
  integrity:sign-app                  Signs an app using a private key.
  integrity:sign-core                 Sign core using a private key.
 l10n
  l10n:createjs                       Create javascript translation files for a given app
 log
  log:file                            manipulate logging backend
  log:manage                          manage logging configuration
 maintenance
  maintenance:data-fingerprint        update the systems data-fingerprint after a backup is restored
  maintenance:mimetype:update-db      Update database mimetypes and update filecache
  maintenance:mimetype:update-js      Update mimetypelist.js
  maintenance:mode                    set maintenance mode
  maintenance:repair                  repair this installation
  maintenance:singleuser              set single user mode
  maintenance:update:htaccess         Updates the .htaccess file
 security
  security:certificates               list trusted certificates
  security:certificates:import        import trusted certificate
  security:certificates:remove        remove trusted certificate
 trashbin
  trashbin:cleanup                    Remove deleted files
  trashbin:expire                     Expires the users trashbin
 twofactorauth
  twofactorauth:disable               Disable two-factor authentication for a user
  twofactorauth:enable                Enable two-factor authentication for a user
 user
  user:add                            adds a user
  user:delete                         deletes the specified user
  user:disable                        disables the specified user
  user:enable                         enables the specified user
  user:info                           show user info
  user:lastseen                       shows when the user was logged in last time
  user:list                           list configured users
  user:report                         shows how many users have access
  user:resetpassword                  Resets the password of the named user
  user:setting                        Read and modify user settings
 versions
  versions:cleanup                    Delete versions
  versions:expire                     Expires the users file versions</pre>
在CentOS中，命令是这样的：
<pre class="lang:sh decode:true ">sudo -u apache php occ</pre>
区别就是Ubuntu和CentOS的http服务器用户不同

## 使用它！

1，遇到一个新命令行工具，我们首先要help一下。
<pre class="lang:sh decode:true ">sudo -u www-data php occ -h
</pre>
输出如下
<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true">Usage:
  help [options] [--] [&lt;command_name&gt;] #格式：help [选项] [--] [命令名]

Arguments:
  command               The command to execute 
  command_name          The command name [default: "help"] #命令名（对应使用格式中的“命令名”）

Options: #选项
      --format=FORMAT   The output format (txt, xml, json, or md) [default: "txt"] #输出格式，默认为txt，下文中有讲
      --raw             To output raw command help #输出原始命令帮助
  -h, --help            Display this help message #显示帮助信息
  -q, --quiet           Do not output any message #不输出任何信息
  -V, --version         Display this application version #显示程序版本
      --ansi            Force ANSI output #强制使用ANSI格式输出
      --no-ansi         Disable ANSI output #禁用ANSI输出
  -n, --no-interaction  Do not ask any interactive question #不要询问任何问题（所有选项默认，大概这个意思）
      --no-warnings     Skip global warnings, show command output only #跳过错误信息
  -v|vv|vvv, --verbose  Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
# 增加消息的详细程度：1用于正常输出，2用于更详细的输出，3用于调试
Help:
 The help command displays help for a given command: #详细地，查看一个命令的使用方法，例如：

   php occ help list

 You can also output the help in other formats by using the --format option:

   php occ help --format=xml list

 To display the list of available commands, please use the list command.</pre>
使用-h选项获取一个命令的详细信息，比如我要查询maintenance:mode（维护模式）命令的使用方式

输入
<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true">sudo -u www-data php occ help maintenance:mode</pre>
<pre class="">Usage:
 maintenance:mode [options] #格式： maintenance:mode+选项（即maintenance:mode后面跟选项）

Options: #选项（对应上面格式中的“选项”）
     --on              enable maintenance mode #激活维护模式
     --off             disable maintenance mode #关闭维护模式
 -h, --help            Display this help message #显示帮助信息，即本段信息
 -q, --quiet           Do not output any message #不输出任何信息
 -V, --version         Display this application version 
     --ansi            Force ANSI output
     --no-ansi         Disable ANSI output
 -n, --no-interaction  Do not ask any interactive question
     --no-warnings     Skip global warnings, show command output only
 -v|vv|vvv, --verbose  Increase the verbosity of messages: 1 for normal output,
                       2 for more verbose output and 3 for debug</pre>
2.显示ownCloud/Nextcloud版本

以Ubuntu、Nextcloud为例
<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true">sudo -u www-data php occ -V #选项为-V，注意大写
  Nextcloud version 9.0.0 #Nextcloud版本为 9.0.0</pre>
3.查询您的Nextcloud服务器状态
<pre class="">sudo -u www-data php occ status
  - installed: true #安装状态：已安装
  - version: 9.0.0.19 #版本：9.0.0.19
  - versionstring: 9.0.0 #版本串：9.0.0
  - edition: #发行版本，社区版不显示，企业版可能会显示</pre>
4.命令输出格式，可以输出txt, xml, json或 md格式的信息

比如以json格式输出服务器状态信息：
<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true">sudo -u www-data php occ status --output=json

{"installed":true,"version":"9.0.0.19","versionstring":"9.0.0","edition":""}</pre>
或者以json_pretty格式输出：
<pre class="">sudo -u www-data php occ status --output=json_pretty
{
   "installed": true,
   "version": "9.0.0.19",
   "versionstring": "9.0.0",
   "edition": ""
}</pre>
（这样，OCC命令可以作为一个API来使用）

5.命令自动补全

Nextcloud11后，OCC命令可以使用自动补全命令，你需要以下命令来设置自动补全
<pre class="lang:sh decode:true "># BASH ~4.x, ZSH
source &lt;(/var/www/html/nextcloud/occ _completion --generate-hook)

# BASH ~3.x, ZSH
/var/www/html/nextcloud/occ _completion --generate-hook | source /dev/stdin

# BASH (any version)
eval $(/var/www/html/nextcloud/occ _completion --generate-hook)</pre>
设置后，只有提供OCC文件完整目录（比如/var/www/html/nextcloud/occ &lt;tab&gt;）才能使用自动补全。在--generate-hook之后指定--programm occ，便可无需在写完整目录。

这样，当你使用OCC命令行工具时，按下Tab键便可自动补全剩余的命令内容。

例如
<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true">输入
sudo -u www-data php occ sta
按Tab键，命令自动补全为：
sudo -u www-data php occ status</pre>

### 插件（APP）管理命令

使用以下命令列出、激活禁用插件
<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true">app
app:check-code check code to be compliant #检查代码是否合法
app:disable disable an app #禁用一个插件（app）
app:enable enable an app #激活一个插件
app:getpath Get an absolute path to the app directory #获取应用程序目录的绝对路径
app:list List all available apps #列出所有可用的插件</pre>
命令示例：
<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true">sudo -u www-data php occ app:list
Enabled:
  - activity: 2.4.1
  - comments: 1.1.0
  - dav: 1.1.1
  - direct_menu: 0.10.0
  - federatedfilesharing: 1.1.1
  - federation: 1.1.1
  - files: 1.6.1
  - files_external: 1.1.2
  - files_markdown: 1.0.0
  - files_pdfviewer: 1.0.1
  - files_sharing: 1.1.1
  - files_texteditor: 2.2
  - files_trashbin: 1.1.0
  - files_versions: 1.4.0
  - files_videoplayer: 1.0.0
  - firstrunwizard: 2.0
  - gallery: 16.0.0
  - logreader: 2.0.0
  - lookup_server_connector: 1.0.0
  - nextcloud_announcements: 1.0
  - notifications: 1.0.1
  - password_policy: 1.1.0
  - provisioning_api: 1.1.0
  - serverinfo: 1.1.1
  - sharebymail: 1.0.1
  - survey_client: 0.1.5
  - systemtags: 1.1.3
  - theming: 1.1.1
  - twofactor_backupcodes: 1.0.0
  - updatenotification: 1.1.1
  - user_saml: 1.2.2
  - workflowengine: 1.1.1
Disabled:
  - admin_audit
  - encryption
  - external
  - files_accesscontrol
  - files_automatedtagging
  - files_retention
  - spreed
  - spreedme
  - templateeditor
  - user_external
  - user_ldap</pre>
1.激活一个插件：
![](https://www.orgleaf.com/wp-content/uploads/2017/01/enable-plugin-occ.png)
<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true">sudo -u www-data php occ app:enable files_automatedtagging #激活此插件

files_automatedtagging enabled
</pre>
![](https://www.orgleaf.com/wp-content/uploads/2017/01/occ-plugin-enabled.png)

禁用插件的方法与此类似

2.app：check-code检查多个项目：它检查应用程序是否使用Nextcloud的公共API（OCP）或私有API（OC_），它还检查已弃用的方法和info.xml文件的有效性。默认情况下启用所有检查。活动应用程式是正确格式的应用程式范例：
<pre class="lang:sh decode:true ">sudo -u www-data php occ app:check-code notifications
App is compliant - awesome job</pre>
如果插件有错误：
<pre class="lang:sh decode:true ">sudo -u www-data php occ app:check-code foo_app
Analysing /var/www/nextcloud/apps/files/foo_app.php
4 errors
   line   45: OCP\Response - Static method of deprecated class must not be
   called
   line   46: OCP\Response - Static method of deprecated class must not be
   called
   line   47: OCP\Response - Static method of deprecated class must not be
   called
   line   49: OC_Util - Static method of private class must not be called</pre>
3.获取插件的绝对目录
<pre class="lang:sh decode:true ">sudo -u www-data php occ app:getpath notifications
/var/www/nextcloud/apps/notifications</pre>

### 选择后台任务执行方式

使用background命令选择要用于控制后台作业（Ajax，Webcron或Cron）的调度程序。这与在您的Nextcloud Admin页面上使用Cron部分相同：
<pre class="lang:sh decode:true ">background
 background:ajax       Use ajax to run background jobs
 background:cron       Use cron to run background jobs
 background:webcron    Use webcron to run background jobs</pre>
例如，选择ajax为后台任务执行方式
<pre class="lang:sh decode:true ">sudo -u www-data php occ background:ajax
  Set mode for background jobs to 'ajax'</pre>
其它的：

*   background:cron
*   background:webcron

### 配置命令

使用config命令来配置服务器：
<pre class="lang:sh decode:true ">config
 config:app:delete      Delete an app config value
 config:app:get         Get an app config value
 config:app:set         Set an app config value
 config:import          Import a list of configs
 config:list            List all configs
 config:system:delete   Delete a system config value
 config:system:get      Get a system config value
 config:system:set      Set a system config value</pre>
列出所有设置值（即配置信息）：
<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true">sudo -u www-data php occ config:list</pre>
列出的内容中隐藏了诸如用户名、密码等信息，可以后加--private参数来显示：
<pre class="lang:sh decode:true ">sudo -u www-data php occ config:list --private</pre>
将配置信息导出为指定格式：
<pre class="lang:sh decode:true ">sudo -u www-data php occ config:list --private</pre>
> P.S.：虽然config命令也可以设置插件的状态，但最好还是用app:命令实现。
获取单个配置信息：
<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true">sudo -u www-data php occ config:system:get version #获取版本信息
9.0.0.19

sudo -u www-data php occ config:app:get activity installed_version #获取一个插件的版本信息
2.2.1</pre>
设置单个配置信息：
<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true">sudo -u www-data php occ config:system:set logtimezone --value="Europe/Berlin" #设置时区
System config value logtimezone set to Europe/Berlin

sudo -u www-data php occ config:app:set files_sharing #设置插件状态
incoming_server2server_share_enabled --value="yes" --type=boolean
Config value incoming_server2server_share_enabled for app files_sharing set to yes</pre>
如果配置信息不存在，在使用config:system:set命令时会自动创建不存在的值。如果你不想它被创建，在后面加上--update-only
<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true">sudo -u www-data php occ config:system:set doesnotexist --value="true"
--type=boolean --update-only
Value not updated, as it has not been set before.</pre>
请注意，为了将布尔值，浮点值或整数值写入配置文件，需要在命令中指定类型。这仅适用于config：system：set命令。以下值是已知的：

*   boolean
*   integer
*   float
*   string (默认)
例如，如果你想禁用维护模式
<pre class="lang:sh decode:true ">sudo -u www-data php occ config:system:set maintenance --value=false
--type=boolean
Nextcloud is in maintenance mode - no app have been loaded
System config value maintenance set to boolean false</pre>

#### 设置不同数组的信息

呃，可能你没理解这是什么意思，以信任域（trust_domains）为例，它在config.php中是这样写的![](https://www.orgleaf.com/wp-content/uploads/2017/01/config-occ-trust-domain.png)

如图，“0”对应第一个信任域“192.168.3.4”，“1”对应第二个信任域“cloud.nosu.win”

那我们可以在设置信任域中直接指定要修改第几个：
<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true">sudo -u www-data php occ config:system:set trusted_domains 1
--value=example.com #指定设置“1”对应的信任域为“example.com”
System config value trusted_domains =&gt; 2 set to string example.com

sudo -u www-data php occ config:system:get trusted_domains
localhost
nextcloud.local
example.com</pre>
在config.php中体现为：

![](https://www.orgleaf.com/wp-content/uploads/2017/01/config-occ-trust-domain2-.png)

#### 删除单个设置值

<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true">sudo -u www-data php occ config:system:delete maintenance:mode #删除maintenance:mode的设置值
System config value maintenance:mode deleted

sudo -u www-data php occ config:app:delete appname provisioning_api
Config value provisioning_api of app appname deleted</pre>
如果设置项本来就不存在，将不会有任何输出，你可以在后面加上--error-if-not-exists来显示错误：
<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true">sudo -u www-data php occ config:system:delete doesnotexist
--error-if-not-exists
Config provisioning_api of app appname could not be deleted because it did not
exist
</pre>

## Dav命令

用于创建地址簿、日历，或在从8.2版本升级至9.0版本时迁移地址簿。

只有使用以下插件时才有必要使用Dav命令：

[![](https://img.orgleaf.com/2017/04/oc-plugin-calendaraddress.png)](https://img.orgleaf.com/2017/04/oc-plugin-calendaraddress.png)

<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="Dav命令">dav
 dav:create-addressbook        #创建一个地址簿
 dav:create-calendar           #创建一个日历
 dav:migrate-addressbooks      #将通讯录从通讯录插件迁移至主通讯录
 dav:migrate-calendars         #将日历从日历插件迁移至主日历
 dav:sync-birthday-calendar    #同步生日日历
 dav:sync-system-addressbook   #将用户同步到系统地址簿
#主通讯录、主日历指ownCloud/Nextcloud自带的通讯录、日历功能dav:create-addressbook</pre>

### 创建/迁移日历和地址簿

<pre class="lang:default decode:1 inline:1 " >dav:creat-calendar和dav:create-addressbook</pre>

 的具体命令格式：

<pre class="lang:default decode:true" title="dav:create-addressbook示例">sudo -u www-data php occ dav:create-addressbook [用户] [名称]

举例：为用户ChengYe创建名为ChengYebook的地址簿
sudo -u www-data php occ dav:create-addressbook ChengYe ChengYebook</pre>

类似的，创建一个新日历的命令为：

<pre class="lang:default decode:true" title="dav:create-carlendar">sudo -u www-data php occ dav:create-calendar [用户] [名称]

举例：为用户ChengYe创建名为Calendar的日历
sudo -u www-data php occ dav:create-calendar ChengYe Celendar</pre>

用户ChengYe会立刻在其日历和联系簿上看到新创建的日历：

[![](https://img.orgleaf.com/2017/04/occ-calendar-create.png)](https://img.orgleaf.com/2017/04/occ-calendar-create.png)

在9.0中，CalDAV服务器已经集成到内核中。升级时，现有的日历和联系人会自动迁移。如果出现问题，可以尝试手动迁移。首先删除任何部分迁移的日历或地址簿。然后运行此命令迁移用户的联系簿：

<pre class="lang:default decode:true" title="迁移地址簿">sudo -u www-data php occ dav:migrate-addressbooks [user]</pre>

迁移用户的日历：

<pre class="lang:default decode:true" title="迁移日历">sudo -u www-data php occ dav:migrate-calendars [user]</pre>

有关故障排除和报告问题的帮助，请参阅 [ownCloud 9.0 - calendar migration analysis](http://morrisjobke.de/2016/03/07/ownCloud-9.0-calendar-migration-analysis/)。

### 同步生日至日历

使用

<pre class="lang:default decode:1 inline:1 " >dav：sync-birthday-calendar</pre>

将所有生日添加到与您共享的地址簿中的日历。此示例为从用户bernie同步到您的日历：

<pre class="lang:default decode:true " title="生日同步">sudo -u www-data php occ dav:sync-birthday-calendar bernie</pre>

使用

<pre class="lang:default decode:1 inline:1 " >dav：sync-system-addressbook</pre>

将所有用户同步到系统地址簿：

<pre class="lang:default decode:true " title="同步至系统地址簿">sudo -u www-data php occ dav:sync-system-addressbook</pre>

## 数据库转换

我们一般使用SQLite来进行小范围（用户单一且不使用同步客户端）的基本测试。但是SQLite的性能不高，对于多个用户的生产服务器，应该使用MariaDB、MySQL或PostgreSQL作为数据库。可以使用OCC命令行工具将SQLite转换为其它类型的数据库。

<pre class="lang:default decode:true" title="数据库转换命令">db
 db:convert-type           #将Nextcloud数据库转换为其它类型
 db:generate-change-script #从当前连接的数据库生成更改脚本至db_structure.xml</pre>

转换数据库类型需要以下条件：
[ssbluelist]

*   所需的数据库及其PHP扩展已安装
*   数据库管理员用户的登录名和密码
*   如果没有使用默认端口号，则需要在命令中写明
[/ssbluelist]

这是将SQLite转换为MySQL / MariaDB的示例：

<pre class="lang:default decode:true " title="转换SQLite至Maraidb/MySQL">sudo -u www-data php occ db:convert-type mysql oc_dbuser 127.0.0.1
oc_database</pre>

## 加密

OCC包括一组完整的管理加密命令：

<pre class="lang:default decode:true" title="加密命令">encryption
 encryption:change-key-storage-root   #修改密钥存储根目录
 encryption:decrypt-all               #禁用服务器端加密并解密所有文件
 encryption:disable                   #禁用服务器端加密
 encryption:enable                    #启用服务器加密
 encryption:enable-master-key         #启用主密钥。仅适用于没有现有加密数据的新安装！还没有办法再次禁用它。
 encryption:encrypt-all               #加密所有用户的所有文件
 encryption:list-modules              #列出所有可用的加密模块
 encryption:migrate                   #初始迁移到2.0加密方式
 encryption:set-default-module        #设置默认模块加密
 encryption:show-key-storage-root     #显示当前密钥存储根目录
 encryption:status                    #列出当前的加密状态</pre>

使用

<pre class="lang:default decode:1 inline:1 " >encryption:status</pre>

 选项可显示是否有激活的加密。要启用加密，必须先启用Encryption 插件，然后运行

<pre class="lang:default decode:1 inline:1 " >encryption:enable</pre>

 。

### 启用Encryption插件

<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="启用Encryption插件">sudo -u www-data php occ app:enable encryption</pre>

也可以在插件管理页面激活加密插件。

### 启用加密

<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="启用加密">sudo -u www-data php occ encryption:enable
sudo -u www-data php occ encryption:status
 - enabled: true
 - defaultModule: OC_DEFAULT_MODULE</pre>

### 转移加密密钥

<pre class="lang:default decode:1 inline:1 " >encryption:change-key-storage-root</pre>

 用于将加密密钥移动到不同的文件夹。在末尾指定新文件夹的位置：

<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="转移加密密钥">sudo -u www-data php occ encryption:change-key-storage-root &lt;新文件夹&gt;</pre>

举例：

<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="转移加密密钥">sudo -u www-data php occ encryption:change-key-storage-root /etc/oc-keys</pre>

你可以通过以下命令来查看密钥文件的位置：

<pre class="lang:sh decode:true " title="查看密钥文件位置">sudo -u www-data php occ encryption:show-key-storage-root
Current key storage root:  default storage location (data/) #密钥当前位于默认目录 (data/)</pre>

### 加密模块

使用

<pre class="lang:default decode:1 inline:1 " >encryption:list-modules</pre>

 可列出所有加密模块（只有启用加密插件后，才会显示模块列表）。使用

<pre class="lang:default decode:1 inline:1 " >encryption:set-default-module [模块名称]</pre>

 来设置默认的加密模块。

### 加密所有用户文件

使用

<pre class="lang:default decode:1 inline:1 " >encryption:encrypt-all</pre>

 来加密所有用户的文件，加密之前，必须要将Nextcloud实例设置为维护模式以阻止所有用户的操作，直到加密完成。

### 文件的解密

<pre class="lang:default decode:1 inline:1 " >encryption:decrypt-all</pre>

 可用于加密所有用户的文件，也可以单独加密某个用户的文件。

示例：

<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="解密特定用户的文件">sudo -u www-data php occ encryption:decrypt freda #解密用户freda的文件</pre>

用户必须在其个人页面上启用恢复密钥。

同样的，解密之前，必须要将Nextcloud实例设置为维护模式以阻止所有用户的操作，直到解密完成。

### 创建主密钥

<pre class="lang:default decode:1 inline:1 " >encryption:enable-master-key</pre>

 创建一个新的主密钥，用于加密所有用户（而不是单个用户）的数据。这对于启用单点登录特别有用。仅在没有数据的刚安装的实例上使用，或者在尚未启用加密的系统上使用此功能。它无法再次被禁用。

### 密钥迁移

<pre class="lang:default decode:1 inline:1 " >encryption:migrate</pre>

 可用于在Nextcloud版本升级后迁移加密密钥。可以为特定用户迁移密钥（多个用户需用空格隔开）。

## Federation Sync（联合云共享服务器的同步）

[infobox]该命令只在Federation插件被激活后可用[/infobox]

同步所有已连接Nextcloud服务器的地址簿：

<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="同步地址簿">federation:sync-addressbooks  #同步所有已连接Nextcloud服务器的地址簿</pre>

在Nextcloud中，共享的服务器之间可以共享用户的通讯录，并在共享对话框中自动补全用户名。使用以下命令来同步联合服务器：

<pre class="lang:sh decode:true " title="同步联合云共享服务器">sudo -u www-data php occ federation:sync-addressbooks</pre>

## 文件操作

occ有三个用于管理Nextcloud中文件的命令:

<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="文件操作">files
 files:cleanup              #清楚文件缓存
 files:scan                 #重新扫描文件系统
 files:transfer-ownership   #将所有文件和文件夹都移动到另一个文件夹</pre>

<pre class="lang:sh decode:1 inline:1 " >files:scan</pre>

命令扫描新文件并更新文件缓存。您可以重新扫描所有文件，各个用户，可以使用空格分隔多个用户，并限制搜索路径。如果不使用

<pre class="lang:default decode:1 inline:1 " >--quiet</pre>

 ，统计信息将在扫描结束时显示：

<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="files:scan">sudo -u www-data php occ files:scan --help
  格式:
  files:scan [-p|--path="..."] [-q|--quiet] [-v|vv|vvv --verbose] [--all]
  [user_id1] ... [user_idN]

参数:
  user_id               #扫描所指定的用户（一个或多个，多个用户ID之间要使用空格分开）的所有文件

选项:
  --path                #限制扫描路径
  --all                 #扫描所有已知用户的所有文件
  --quiet               #不输出统计信息
  --verbose             #在扫描过程中显示正在处理的文件和目录
  --unscanned           #仅扫描以前未扫描过的文件</pre>

<pre class="lang:default decode:1 inline:1 " >-vv</pre>

 或

<pre class="lang:default decode:1 inline:1 " >-vvv</pre>

的详细级别会自动重置为

<pre class="lang:default decode:1 inline:1 " >-v</pre>

关于选项

<pre class="lang:default decode:1 inline:1 " >--unscanned</pre>

 ：一般情况下，这个命令会通过后台任务（使用cron实现）执行，定期扫描文件。这个“扫描”选项可以从CLI触发。

### 指定扫描位置

当使用

<pre class="lang:default decode:1 inline:1 " >--path</pre>

 选项时，该路径必须包含以下部分：

<pre class="lang:default decode:true">"user_id/files/path"
  或
"user_id/files/mount_name"
  或
"user_id/files/mount_name/path"</pre>

其中，

<pre class="lang:default decode:1 inline:1 " >files</pre>

 是必须要加上的，不可忽略。

示例：

<pre class="lang:default decode:true">--path="/alice/files/Music" #指向用户alice的Music文件夹</pre>

在上面的示例中，

<pre class="lang:default decode:1 inline:1 " >user_id</pre>

 对应的用户是唯一的（也就是alice），同样，

<pre class="lang:default decode:1 inline:1 " >--path</pre>

 ，

<pre class="lang:default decode:1 inline:1 " >--all</pre>

的参数也是唯一的（有且仅能有一个参数）。

### 清除缓存

<pre class="lang:default decode:1 inline:1 " >files:cleanup</pre>

 通过删除存储表中没有匹配条目的文件来清理服务器的文件缓存。

### 用户间文件迁移

您可以将所有文件和共享从一个用户传输到另一个用户。这在删除用户之前很有用：

<pre  lang="bash" line="1" escaped="true" lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="文件的迁移">sudo -u www-data php occ files:transfer-ownership &lt;来源用户&gt; 
&lt;目标用户&gt;</pre>

## 外部存储

[infobox]该命令只在[External storage support](https://www.orgleaf.com/843.html)插件 (`<span class="pre">files_external</span>`)被激活后可用[/infobox]

用于管理外部存储的命令：

<pre class="lang:default decode:true " title="外部存储管理">files_external
 files_external:applicable  #管理可使用挂载的用户和组（不是很明白）
 files_external:backends    #显示可用的身份验证方式和存储后端
 files_external:config      #管理挂载点的后端配置
 files_external:create      #创建一个新的挂载配置
 files_external:delete      #删除一个已挂载的外部存储
 files_external:export      #导出挂载配置
 files_external:import      #导入挂载配置
 files_external:list        #列出已配置完成的外部存储
 files_external:option      #管理外部存储的挂载选项
 files_external:verify      #校验挂载配置
 files_external:notify      #监听配置的外部安装的活动更新通知</pre>

这些命令的功能Nextcloud Web GUI中的功能相同，除此之外还有两个新功能：

<pre class="lang:default decode:1 inline:1 " >files_external:export</pre>

 和

<pre class="lang:default decode:1 inline:1 " >files_external:import</pre>

 。

使用

<pre class="lang:default decode:1 inline:1 " >files_external:export</pre>

将所有管理员挂载导出到stdout，或使用

<pre class="lang:default decode:1 inline:1 " >files_external:export [user_id]</pre>

 导出指定的Nextcloud用户的挂载。

使用

<pre class="lang:default decode:1 inline:1 " >files_external:import [filename]</pre>

 导入旧的JSON配置，并将外部装载配置复制到另一台Nextcloud服务器。

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
