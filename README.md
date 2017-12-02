# Nextcloud文档汉化项目
我的博客 [橙叶博客](https://www.orgleaf.com)
Nextcloud仅提供了英文文档，为了方便国内的想尝试Nextcloud朋友，决定对Nextcloud的文档进行汉化。目前仅处于启动阶段。

## 当前汉化状况
- 仅完成极少部分汉化
- 已完成的汉化的文档在博客教程的基础上稍作修改而成，与官方文档有一定区别，无法做到100%对应
- 原文章为HTML格式，直接转换为了MD，存在语法错误

## 汉化需求
我希望能有人来帮我完成汉化，在汉化的同时可以充分了解Nextcloud的功能。
- 使用MarkDown撰写
- 内容格式与官方文档基本对应
- 图片尽量更换为含中文的图片
- 由于中文与英文存在较大差异，个别句子、段落采取意译

## 已汉化的文档
```
├─ admin_manual
│  ├─ configuration_database
│  │  ├─ bigint_identifiers.rst
│  │  ├─ db_conversion.rst
│  │  ├─ index.rst
│  │  ├─ linux_database_configuration.rst
│  │  └─ mysql_4byte_support.rst
│  ├─ configuration_files
│  │  ├─ external_storage
│  │  │  ├─ amazons3.rst
│  │  │  ├─ auth_mechanisms.rst
│  │  │  ├─ dropbox.rst
│  │  │  ├─ ftp.rst
│  │  │  ├─ google.rst
│  │  │  ├─ local.rst
│  │  │  ├─ nextcloud.rst
│  │  │  ├─ openstack.rst
│  │  │  ├─ sftp.rst
│  │  │  ├─ smb.rst
│  │  │  └─ webdav.rst
│  │  ├─ big_file_upload_configuration.rst ->大文件上传配置.md
│  │  ├─ default_files_configuration.rst
│  │  ├─ encryption_configuration.rst
│  │  ├─ external_storage_configuration.rst
│  │  ├─ external_storage_configuration_gui.rst
│  │  ├─ federated_cloud_sharing_configuration.rst
│  │  ├─ file_sharing_configuration.rst
│  │  ├─ file_versioning.rst
│  │  ├─ files_locking_transactional.rst
│  │  ├─ index.rst
│  │  ├─ previews_configuration.rst
│  │  └─ primary_storage.rst
│  ├─ configuration_mimetypes
│  │  └─ index.rst
│  ├─ configuration_server
│  │  ├─ activity_configuration.rst
│  │  ├─ antivirus_configuration.rst
│  │  ├─ automatic_configuration.rst   -> 自动配置.md
│  │  ├─ background_jobs_configuration.rst
│  │  ├─ caching_configuration.rst
│  │  ├─ config_sample_php_parameters.rst
│  │  ├─ custom_client_repos.rst
│  │  ├─ email_configuration.rst
│  │  ├─ external_sites.rst
│  │  ├─ harden_server.rst
│  │  ├─ index.rst
│  │  ├─ knowledgebase_configuration.rst
│  │  ├─ language_configuration.rst
│  │  ├─ logging_configuration.rst
│  │  ├─ occ_command.rst                -> OCC命令.md
│  │  ├─ reverse_proxy_configuration.rst
│  │  ├─ security_setup_warnings.rst    -> 安全设置警告.md
│  │  ├─ server_tuning.rst
│  │  ├─ sso_configuration.rst
│  │  ├─ theming.rst
│  │  └─ thirdparty_php_configuration.rst
│  ├─ configuration_user
│  │  ├─ index.rst
│  │  ├─ instruction_set_for_apps.rst
│  │  ├─ instruction_set_for_groups.rst
│  │  ├─ instruction_set_for_users.rst
│  │  ├─ reset_admin_password.rst
│  │  ├─ reset_user_password.rst
│  │  ├─ two_factor-auth.rst
│  │  ├─ user_auth_ftp_smb_imap.rst
│  │  ├─ user_auth_ldap.rst
│  │  ├─ user_auth_ldap_api.rst
│  │  ├─ user_auth_ldap_cleanup.rst
│  │  ├─ user_configuration.rst
│  │  ├─ user_password_policy.rst
│  │  └─ user_provisioning_api.rst
│  ├─ file_workflows
│  │  ├─ access_control.rst
│  │  ├─ automated_tagging.rst
│  │  ├─ index.rst
│  │  └─ retention.rst
│  ├─ installation
│  │  ├─ apps_management_installation.rst
│  │  ├─ apps_supported.rst
│  │  ├─ command_line_installation.rst
│  │  ├─ deployment_recommendations.rst
│  │  ├─ index.rst
│  │  ├─ installation_wizard.rst
│  │  ├─ nginx.rst
│  │  ├─ selinux_configuration.rst
│  │  ├─ source_installation.rst
│  │  └─ system_requirements.rst
│  ├─ issues
│  │  ├─ code_signing.rst
│  │  ├─ general_troubleshooting.rst
│  │  └─ index.rst
│  ├─ maintenance
│  │  ├─ backup.rst
│  │  ├─ index.rst
│  │  ├─ manual_upgrade.rst
│  │  ├─ migrating.rst
│  │  ├─ migrating_owncloud.rst  ->从ownCloud迁移（需修正）.md
│  │  ├─ package_upgrade.rst
│  │  ├─ restore.rst
│  │  ├─ update.rst
│  │  └─ upgrade.rst
│  ├─ operations
│  │  ├─ considerations_on_monitoring.rst
│  │  ├─ index.rst
│  │  └─ scaling_multiple_machines.rst
│  ├─ Create HTML.lnk
│  ├─ Create PDF.lnk
│  ├─ Makefile
│  ├─ conf.py
│  ├─ contents.rst
│  ├─ index.rst
│  ├─ make.bat
│  └─ release_notes.rst
├─ developer_manual
│  ├─ android_library
│  │  ├─ examples.rst
│  │  ├─ index.rst
│  │  └─ library_installation.rst
│  ├─ app
│  │  ├─ api.rst
│  │  ├─ appdata.rst
│  │  ├─ backgroundjobs.rst
│  │  ├─ changelog.rst
│  │  ├─ classloader.rst
│  │  ├─ code_signing.rst
│  │  ├─ configuration.rst
│  │  ├─ container.rst
│  │  ├─ controllers.rst
│  │  ├─ css.rst
│  │  ├─ database.rst
│  │  ├─ filesystem.rst
│  │  ├─ hooks.rst
│  │  ├─ index.rst
│  │  ├─ info.rst
│  │  ├─ init.rst
│  │  ├─ js.rst
│  │  ├─ l10n.rst
│  │  ├─ logging.rst
│  │  ├─ middleware.rst
│  │  ├─ publishing.rst
│  │  ├─ repair.rst
│  │  ├─ request.rst
│  │  ├─ routes.rst
│  │  ├─ schema.rst
│  │  ├─ settings.rst
│  │  ├─ startapp.rst
│  │  ├─ templates.rst
│  │  ├─ testing.rst
│  │  ├─ theming.rst
│  │  ├─ tutorial.rst
│  │  ├─ two-factor-provider.rst
│  │  └─ users.rst
│  ├─ bugtracker
│  │  ├─ codereviews.rst
│  │  ├─ index.rst
│  │  ├─ kanban.rst
│  │  └─ triaging.rst
│  ├─ client_apis
│  │  ├─ OCS
│  │  │  └─ index.rst
│  │  ├─ WebDAV
│  │  │  └─ index.rst
│  │  └─ index.rst
│  ├─ commun
│  │  └─ index.rst
│  ├─ core
│  │  ├─ configfile.rst
│  │  ├─ externalapi.rst
│  │  ├─ index.rst
│  │  ├─ ocs-share-api.rst
│  │  ├─ theming.rst
│  │  ├─ translation.rst
│  │  └─ unit-testing.rst
```
