[![](https://img.orgleaf.com/2017/08/owncloud-before-migarin.png)](https://img.orgleaf.com/2017/08/owncloud-before-migarin.png)

## 法一：使用迁移脚本

这是比较简单省力的方法，Nextcloud提供了用于迁移的各项脚本。这个脚本支持ownCloud 8.2~10.0版本。

迁移之前首先要明确一点：你的ownCloud装在了哪里？

这是个很简单的问题，但是仍然有必要确定清楚，一般的，ownCloud会放在
<pre class="lang:default decode:1 inline:1 ">/var/www/html</pre>
里。也许它装在子目录（不推荐），比如
<pre class="lang:default decode:1 inline:1 ">/var/www/html/owncloud</pre>
，当然还可以是其他目录，比如
<pre class="lang:default decode:1 inline:1 ">/cloudserver/owncloud</pre>
。在ownCloud的Docker镜像中，
<pre class="lang:default decode:1 inline:1 ">ownCloud被安装在/var/www/html</pre>
。

确定这点之后，进入安装目录：
<pre class="lang:sh decode:true ">cd /安/装/目/录</pre>
[![](https://img.orgleaf.com/2017/08/cd-owncloud-install-fold.png)](https://img.orgleaf.com/2017/08/cd-owncloud-install-fold.png)下载

下载Nextcloud提供的迁移工具：
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="下载迁移工具">wget https://download.nextcloud.com/server/installer/migrator/index.php</pre>
因为在安装目录中已经存在一个index.php了，所以下载的脚本会被自动重命名为index.php.1。接下来将下载好的文件重命名为index.php并放到
<pre class="lang:default decode:1 inline:1 ">updater</pre>
文件夹中:
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="安装迁移工具">mv index.php.1 updater/index.php</pre>
完成之后设置权限（
<pre class="lang:default decode:1 inline:1 ">www-data</pre>
是HTTP服务器的用户和组）：
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="设置权限">chmod 750 updater/index.php &amp;&amp; chown www-data:www-data updater/index.php</pre>
在浏览器中登录ownCloud，然后访问刚才下载的脚本，例如：
<pre class="lang:default decode:1 inline:1 ">https://your.owncloudserver.com/updater/index.php</pre>
[![](https://img.orgleaf.com/2017/08/access-nextcloud-migrate-tools.png)](https://img.orgleaf.com/2017/08/access-nextcloud-migrate-tools.png)

[infobox]确保你的ownCloud版本小于10.0.2，不然会出现Could not determine migration path to Nextcloud.的错误。这个BUG在未来可能会被修复[/infobox]

点击“Start update”开始迁移：

[![](https://img.orgleaf.com/2017/08/start-update-lala.png)](https://img.orgleaf.com/2017/08/start-update-lala.png)

然后创建备份、下载Nextcloud（时间可能会比较长）。

[![](https://img.orgleaf.com/2017/08/migrating-to-nextcloud.png)](https://img.orgleaf.com/2017/08/migrating-to-nextcloud.png)

对于ownCloud9.1.6版本，在解压时可能会出现一个错误：

[![](https://img.orgleaf.com/2017/08/error-dowver-lower-than-installed.png)](https://img.orgleaf.com/2017/08/error-dowver-lower-than-installed.png)

&nbsp;

这个错误挺尴尬的。解决方法是将ownCloud的版本手动设置为9.1.5。编辑config/config.php
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true">vim config/config.php

将
'version' =&gt; '9.1.6.2',
改为
'version' =&gt; '9.1.5.2',</pre>
&nbsp;

[![](https://img.orgleaf.com/2017/08/2017-08-25_15h51_30.png)](https://img.orgleaf.com/2017/08/2017-08-25_15h51_30.png)

保存退出，刷新浏览器页面。

[![](https://img.orgleaf.com/2017/08/change-version-to-9152.png)](https://img.orgleaf.com/2017/08/change-version-to-9152.png)

[infobox]因为ownCloud9.1.5和9.1.6版本稍有不同，所以这不是一个值得推荐的方法。更好的方法可以参考后文中有关手动迁移的内容。[/infobox]

[![](https://img.orgleaf.com/2017/08/download-and-extracyying-success.png)](https://img.orgleaf.com/2017/08/download-and-extracyying-success.png)

选择
<pre class="lang:default decode:1 inline:1 ">No(for usage of the web based updater)</pre>
，关闭维护模式。[![](https://img.orgleaf.com/2017/08/go-to-nextcloud-finised.png)](https://img.orgleaf.com/2017/08/go-to-nextcloud-finised.png)

在打开的页面中点击“开始更新”：

[![](https://img.orgleaf.com/2017/08/start-to-upgrade-oc-to-nc.png)](https://img.orgleaf.com/2017/08/start-to-upgrade-oc-to-nc.png)

[![](https://img.orgleaf.com/2017/08/2017-08-25_16h01_43.png)](https://img.orgleaf.com/2017/08/2017-08-25_16h01_43.png)

稍后，页面会自动跳转，你可以看到ownCloud已经被换成Nextcloud，所有的数据和文件都已经完成自动迁移。

[![](https://img.orgleaf.com/2017/08/2017-08-25_16h02_57.png)](https://img.orgleaf.com/2017/08/2017-08-25_16h02_57.png)

个别图标仍是ownCloud的样式，清除浏览器缓存即可。

## 法二：手动迁移

相比之下，手动迁移更加灵活，步骤类似手动升级ownCloud。

### 1.启用维护模式

用OCC命令行工具启用维护模式：
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="开启维护模式">sudo -u www-data php occ maintenance:mode --on</pre>
也可以在config.php中手动设置。在config/config.php里添加这样一行：
<pre class="lang:php decode:true" title="开启维护模式">'maintenance' =&gt; true,</pre>
[![](https://img.orgleaf.com/2017/08/add-maintenance-ture0configophp.png)](https://img.orgleaf.com/2017/08/add-maintenance-ture0configophp.png)

访问ownCloud，看看维护模式是否已经开启是

### 2.备份设置和数据库

这个步骤主要是为了以防万一。

需要备份的是data目录和config目录，而里面分别存放这数据和设置。
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="备份数据和设置">cp config/config.php /home/config.php.bk 
cp data /home/databk -rf</pre>
然后备份数据库（假设数据库名为nextcloud）：
<pre class="lang:mysql decode:true" title="备份数据库">mysqldump -u root -p nextcloud&gt;nextcloud.sql，</pre>
恢复方法：
<pre class="lang:mysql decode:true " title="恢复数据库">mysql -u root -p

mysql&gt;show database;                #查看数据库是否还存在
mysql&gt;create database nextcloud;    #创建缺失的数据库
mysql&gt;use nextcloud;                #切换数据库
mysql&gt;source nextcloud.sql;          #恢复数据库</pre>

* * *

P.S.:如果你使用的是SQLite数据库，SQLite在迁移后会出现丢失的情况。你需要在迁移之前将SQLite转换成MySQL或者MariaDB：
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="转换数据库">sudo -u www-data php occ db:convert-type [options] type username hostname database</pre>

*   username:数据库用户名
*   hostname:MySQL的地址
*   database:数据库名
示例：
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="示例">php occ db:convert-type --all-apps mysql oc_mysql_user 127.0.0.1 new_db_name</pre>
转换之后再按照上文的步骤备份数据库。

### 3.更换程序源码

为了方便些，先将需要保留的文件都迁移出来：
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="迁移需要保留的文件">cp config/config.php /home/config.php.bk
cp data /home/databk -rf</pre>
然后清空目录：
<pre class="lang:sh decode:true " title="清空目录">rm * -Rf</pre>
下载Nextcloud，ownCloud与Nextcloud版本有对应关系，参照下表下载相应的版本的Nextcloud:

[ssbluelist]

*   ownCloud 8.0.x -&gt; ownCloud 8.1.x -&gt; ownCloud 8.2.x -&gt; Nextcloud 9.0.x -&gt; Nextcloud 10.0.x
*   ownCloud 8.2.x -&gt; Nextcloud 9.0.x -&gt; Nextcloud 10.0.x
*   ownCloud 9.0.x -&gt; Nextcloud 9.0.x -&gt; Nextcloud 10.0.x
*   ownCloud 9.1.x -&gt; Nextcloud 10.0.x -&gt; Nextcloud 11.0.x
*   ownCloud 10.0.- -&gt; Nextcloud 12.0.0
[/ssbluelist]

例如我的ownCloud版本是9.1.5，我需要下载Nextcloud 11.0.x
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="下载相应的Nextcloud">wget https://download.nextcloud.com/server/releases/nextcloud-11.0.2.zip
</pre>
解压、迁移文件：
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="解压">unzip nextcloud-11.0.2.zip -d /var/www/
mv /var/www/nextcloud/* /var/www/html/

调整文件权限
chown -R www-data:www-data /var/www/html
find /var/www/html/ -type d -exec chmod 750 {} \;
find /var/www/html/ -type f -exec chmod 640 {} \;</pre>
迁移配置文件：
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="迁移备份文件">cp /home/config.php.bk /var/www/html/config/config.php
cp /home/databk /var/www/html/data -rf       #data目录的位置由你在ownCloud中的设置决定</pre>
关闭维护模式：

方法1：使用OCC命令

<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="关闭维护模式" style="padding-left: 30px;">sudo -u www-data php occ maintenance:mode --off</pre>

方法2：修改config.php

将config/config.php中之前所添加的

<pre class="lang:default decode:1 inline:1 ">'maintenance' =&gt; true,</pre>
改为
<pre class="lang:default decode:1 inline:1 ">'maintenance' =&gt; false,</pre>
。

[infobox]如果在迁移之前使用的是SQLite数据库，那么在迁移的时候会出现
<pre class="lang:default decode:1 inline:1 ">An unhandled exception has been thrown: exception 'PDOException' with message 'SQLSTATE[HY000]: General error: 1 no such table: oc_appconfig' in /var/www/html/3rdparty/doctrine/dbal/lib/Doctrine/DBAL/Driver/PDOConnection.php:104</pre>
的错误[/infobox]

在浏览器中访问ownCloud，点击“开始更新”。

[![](https://img.orgleaf.com/2017/08/ready-for-upgeade-oc-to-nc.png)](https://img.orgleaf.com/2017/08/ready-for-upgeade-oc-to-nc.png)

[![](https://img.orgleaf.com/2017/08/updating-to-nc.png)](https://img.orgleaf.com/2017/08/updating-to-nc.png)

你也可以执行以下命令：
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="更新命令">sudo -u www-data:www-data php occ upgrade</pre>
因为ownCloud和Nextcloud有一些插件不兼容，所以在升级为Nextcloud时，个别插件会被禁用。

[![](https://img.orgleaf.com/2017/08/finishe-upgrade-oc-to-nc.png)](https://img.orgleaf.com/2017/08/finishe-upgrade-oc-to-nc.png)

点击“继续访问Nextcloud”，就可以使用Nextcloud了。

## 文件完整性检查错误

在迁移文件时可能会出现.htaccess文件没有迁移的情况。在校验文件完整性时就会报错。

[![](https://img.orgleaf.com/2017/08/dai-ma-wanzhengxing.png)](https://img.orgleaf.com/2017/08/dai-ma-wanzhengxing.png)
<pre class="height-set:true height:300 lang:default decode:true" title="无效文件列表">Technical information
=====================
The following list covers which files have failed the integrity check. Please read
the previous linked documentation to learn more about the errors and how to fix
them.

Results
=======
- core
    - INVALID_HASH
        - .htaccess

Raw output
==========
Array
(
    [core] =&gt; Array
        (
            [INVALID_HASH] =&gt; Array
                (
                    [.htaccess] =&gt; Array
                        (
                            [expected] =&gt; 11e2db30f0cf23df1b5aa1cdf329a8c88d253f86e43f9e7af1b30969eb0175030103b138e2f7ab7608c902bbb57a5d578c2c0ca09f3abf2ef83415f4bc6f6e20
                            [current] =&gt; 9e034bf735877287df33d6ee93465c62c23727a90ed71d1731a7448d239a44054b37c582bb85949307e161d18cfd14420383f55c4862aa8b4975181270e4a761
                        )

                )

        )

)</pre>
我们可以看到.htaccess文件的哈希码错误。解决方法很简单，从Nextcloud安装包中拷贝一个.htaccess过去即可。
<pre lang="bash" line="1" escaped="true" class="lang:sh decode:true" title="解决代码完整性检查错误">rm /var/www/html/.htaccess    #删除当前的.htaccess文件
cp -r nextcloud/.htaccess /var/www/html  #将安装包内的.htaccess文件拷贝到目录中</pre>
点击重新扫描：

[![](https://img.orgleaf.com/2017/08/resacn-files-error.png)](https://img.orgleaf.com/2017/08/resacn-files-error.png)

可以看到文件完整性检查的错误信息已经消失。

[![](https://img.orgleaf.com/2017/08/success-to-solve-files-error.png)](https://img.orgleaf.com/2017/08/success-to-solve-files-error.png)
