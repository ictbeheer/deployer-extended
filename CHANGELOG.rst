
Changelog
---------

24.1.1
------

1) [BUGFIX] Fix the logic for resolving PHP binary. If the binary specified by ``php_version`` or ``composer.json``
   is not found, it now gracefully falls back to search for ``php`` binary and finally defaults to plain ``php``.

24.1.0
------

a) [TASK][FEATURE] Print http status code for curl in cache:clear_php_http (credits to `martipoe <https://github.com/martipoe>`_ )

24.0.0
------

a) [TASK][BREAKING] Move ``service_php_fpm_reload.php`` from ``includes/`` to auto loaded ``deployer/service/service_php_fpm_reload.php``.

23.0.0
------

a) [TASK][BREAKING] Remove declaration of ``set('web_path', '');`` as it creates problems with overriding if other
   packages use the same name. Breaking change, because if this setting was used outside this package then now will be null,
   but was empty string.

22.0.0
------

a) [FEATURE] Add ``bin/php`` that enhance standard behaviour of Deployer. It will check for
   ``php_version`` in host settings and if not found then it will check for ``['config']['platform']['php']``
   and ``['require']['php']`` in composer.json. If not found then it will fallback to standard ``php``.

b) [TASK][BREAKING] Enhance existing ``local/bin/php`` to check for ``php_version`` in host settings and
   if not found then it will check for ``['config']['platform']['php']`` and ``['require']['php']`` in
   composer.json. If not found then it will fallback to standard ``php``. This can return different version of PHP so
   breaking change.

c) [TASK][BREAKING] Move ``bin/composer`` override to ``includes/settings/bin_composer.php``. This is breaking change as path
    has changed and this file is loaded manually.

d) [FEATURE] Add fixed version of original "release" task (https://github.com/deployphp/deployer/pull/4034) which will
   be available only to Deployer 8. Use if you still need it for Deployer 7.

e) [FEATURE] Add simple task for php-fpm reloading. Make it hidden by default.

f) [TASK][BREAKING] Remove deprecated eaccelerator calls.

21.0.0
------

a) [BUGFIX] Remove dependency to ``argument_host`` which was part of removed ``sourcebroker/deployer-instance``.
b) [TASK][BREAKING] Remove overwriting of ``branch`` setting. This should be done at higher level. Base should follow Deployer
   default.
c) [TASK][BREAKING] Remove overwriting of ``bin/composer`` setting. Base should be Deployer default. If you want then include
   ``includes/composer.php`` file directly in your project.
d) [TASK][BREAKING] Make all task hidden as they should be usually part of deploy task. If you want to unhide task then
   ``task('taskname')->hidden(false);`` in your deploy.php file.
e) [TASK][BREAKING] Rename ``current_dir`` setting to ``project_root`` to reflect real usage.
f) [TASK][BREAKING] Remove ``random`` setting to not pollute global Deployer scope without a good reason. After recent
   cleanup on tasks the ``random`` setting was used only at one task ``cache:clear_php_http``.

20.0.0
~~~~~~

a) [TASK][BREAKING] Remove dependency to ``sourcebroker/deployer-instance``. Not needed anymore.
b) [TASK][BREAKING] Remove task ``buffer:start``, ``buffer:stop`` as hard to test on so many hoster configs and different level of traffic.
c) [TASK][BREAKING] Remove task ``file:rm2steps:1``, ``file:rm2steps:2`` as should be not needed for nowadays deployment flow.
d) [FEATURE] Add task ``upload_build``.

19.0.0
~~~~~~

a) [TASK][BREAKING] Replace ``--ignore-platform-reqs`` with ``{{check_composer_install_options}}`` in ``deploy:check_composer_install``
    This change allows for greater flexibility in managing the options for ``composer install --dry-run``.
    Default Value:
    ``--no-dev --no-interaction --no-progress --no-suggest --no-scripts --no-plugins``
    Note:
    The value for ``{{check_composer_install_options}}`` must differ from ``{{composer_options}}``, as the latter
    has ``--no-dev`` by default. Using ``--no-dev`` in local development would remove require-dev packages.

b) [FEATURE] Add `deploy:check_composer_validate` task.

18.0.0
~~~~~~

a) [TASK][BREAKING] Bump dependency to ``sourcebroker/deployer-instance``.

b) [TASK] Clean up code.

17.0.0
~~~~~~

a) [TASK] Code refactor. Change Exception to GracefulShutdownException. Casting optimisation. Code reformatting / cleanup.

b) [BREAKING] Remove task ``deploy_extend_log`` as it is now part of Deployer 7. Refactor task `deploy_check_branch`
   to check extended data deployer meta data file.

c) [TASK] Refactor code for Deployer 7.

d) [TASK] Update dependencies for Deployer 7.

e) [TASK] Extend dependency to internal packages to dev-master.

16.1.0
~~~~~~

a) [BUGFIX] For task ``cache:clear_php_http`` add ``--no-check-certificate`` for wget (curl already have ``--insecure``)

b) [FEATURE] For task ``cache:clear_php_http`` add ``fetch_method_wget_options`` and ``fetch_method_curl_options``.

16.0.0
~~~~~~

a) [FEATURE][BREAKING] Overwrite "bin/composer" and allow to setup composer binary version with ``composer_version``
   or ``composer_channel``.  The default setting are: ``composer_version=null`` and ``composer_channel="stable"``.
   This will download most new stable version of composer (for now version 2).

b) [TASK][BREAKING] For task ``deploy_check_composer_install`` local version of composer must be available. So far it was
   downloaded in ``set('local/bin/composer')``. Since this change there will be no try to download it. Composer must be
   installed and accessible locally for user running commands.

c) [BUGFIX] Fix check if composer install must be run because of composer.lock changes.

15.0.0
~~~~~~

a) [TASK][BREAKING] Remove config:vhost_apache task without replacement. Use ``https://ddev.readthedocs.io/en/stable/``
   or similar solutions for local development.

b) [TASK][BREAKING] Add dependency to breaking ``sourcebroker/deployer-instance``.

c) [TASK] Add ddev support.

14.1.0
~~~~~~

a) [FEATURE] Add task ``file:copy_dirs_ignore_existing`` which copy directories from previous release except for those
    folders which already exists in that folder.

b) [FEATURE] Add task ``file:copy_files_ignore_existing`` which copy files from previous release except for those
    files which already exists in that folder.

14.0.1
~~~~~~~

a) [BUGFIX] Fix refactor of composer binary detection.

14.0.0
~~~~~~~

a) [TASK][BREAKING] Change default php-fpm directive from ProxyPass to SetHandler in task ``config vhost_apache``.
b) [BUGFIX] Add support for ``web_path`` added to ``vhost_document_root`` in task ``config vhost_apache``.
c) [TASK] Refactor way the binary is detected. Possible breaking change.

13.0.0
~~~~~~

a) [TASK][BREAKING] Change to new deployer-instance version.
b) [TASK][BREAKING] Set naming according to new deployer-instance.

12.0.0
~~~~~~

a) [BUGFIX] Compatibility with 6+. Fix local test for composer.json in config_vhost_apache.php.
b) [BUGFIX] Fix wrong calculation for vhost_local_logs_path.
c) [BUGFIX] Fix test of existence for symlinked log files.
d) [TASK] Refactor deploy:check_branch task.
e) [TASK] Add deploy:check_branch_local task.
f) [BUGFIX] Fix condition in deploy:check_branch_local task.
g) [BUGFIX] Move cd() before condition in deploy_check_branch.php
h) [TASK] Add ability to turn of branch guess which is by default added to deployer. By setting "branch_detect_to_deploy" you can disable deploying currently checkout branch.
i) [TASK] Refactor deploy:extend_log to support for revision and tag options.
j) [TASK] Support to show time of deployment in deployment note.

11.0.1
~~~~~~

a) [BUGFIX] Fix wrong detection of previous clear http cache file.

11.0.0
~~~~~~

a) [TASK][BREAKING] Rename task php:clear_cache_cli.php to cache:clear_php_cli and php:clear_cache_http.php to cache:clear_php_http
b) [TASK][BREAKING] Rename the logs filename to .dep/releases.extended. Add hash to log line. Format log line with csv formatter.
c) [TASK][BREAKING] Deployer 6.4+ compatibility.

10.0.2
~~~~~~

a) [BUGFIX] Replace colon in filenames with underscore for Windows compatibility.

10.0.1
~~~~~~

a) [BUGFIX] Fix wrong formatting for info form deploy:check_branch task. Add GracefulShutdownException.

10.0.0
~~~~~~

a) [BUGFIX] Replace colon in filenames with underscore for Windows compatibility.
b) [FEATURE] Add task deploy:check_branch to check if branch deployed to instance is the same as the one which is being deployed.
c) [FEATURE] Add task extend:log to store additional info about deploy.
d) [TASK] Increase version of sourcebroker/deployer-instance
e) [TASK] Normalize use of dots at the end of task description.

9.1.0
~~~~~

a) [FEATURE] Add possibility to set "vhost_document_root" outside.

9.0.0
~~~~~

a) [BUGFIX][BREAKING] Fix wrong flag name for old release and prevent creation of this flag if current folder does not exits.
b) [BUGFIX][BREAKING] Create "old release" flag just before removing "buffer request" flag.
c) [TASK] Refactor buffer:stop
d) [TASK][BREAKING] Remove composer dependencies to sourcebroker/deployer-loader. It must be declared in higher level package as
   someone can use task without autoloader.
e) [TASK][BREAKING] Refactor config:vhost_apache with possible breaking changes.
f) [TASK] Refactor config:vhost_apache.

8.0.1
~~~~~

a) [BUGFIX] Remove unneeded comments.
b) [DOCS] Docs cleanup.

8.0.0
~~~~~

a) [TASK][!!!BREAKING] Remove default set('fetch_method', 'wget'); as it should have fallback in task itself.
b) [BUGFIX] Create lock file in buffer:start only when directory exists.
c) [TASK] Tasks buffer:start, buffer:stop code cleanup.
d) [TASK][!!!BREAKING] Remove multiplexing on from deployer-extended default config vars as it should be part of higher
   level package.
e) [TASK][!!!BREAKING] Remove FileUtility class to make tasks more independent. The method usage from this class
   usage was not really big in the end.
f) [TASK][!!!BREAKING] Refactor config:vhost_apache task. Start of docs for this task.
g) [TASK] Rewrite log file creation for config:vhost_apache.
h) [TASK] Change composer.json description. Remove psr-4 as no classes.
i) [TASK] Add support for edge cases in config:vhost_apache task.
j) [TASK] Task config:vhost_apache - add more descriptive user messages for different missing data cases.
k) [TASK] Task config:vhost_apache - convert all files operation to runLocally / testLocally.
l) [TASK] Cleanup code on task ``config:vhost_apache``
m) [FEATURE] Implement extended flags in buffer:start with flags that cleans php stat cache for specific amount of time,
   and lock which is doing redirects if it detects that it still pointing to old release.

7.1.3
~~~~~

a) [DOCS] Update changelog.


7.1.2
~~~~~

a) [BUGFIX] In task "buffer:start" add -f (force) to mv command as on some linux distro its asking to overwrite by default.

7.1.1
~~~~~

a) [BUGFIX] Fix wrongly set default fetch_method for "php:clear_cache_http"
b) [DOC] Update changelog.

7.1.0
~~~~~

a) [FEATURE] Add curl as additional fetch_method.
b) [FEATURE] Add fallback when fetch_method is not set.
c) [BUGFIX] Change wget command to not store file at all. Previous settings causes wget to return error
   when there was no access to write on current folder. Right now there is no need to have write
   access.
d) [BUGFIX] Do fallback for get('public_urls', []) so right exception is shown.
e) [FEATURE] Introduce {{bin/local/wget}}
f) [FEATURE] Introduce {{bin/local/curl}}
g) [DOC] Extend documentation about task properties.

7.0.0
~~~~~

a) [TASK] Add dependency to sourcebroker/deployer-loader
b) [TASK][!!!BREAKING] Remove SourceBroker\DeployerExtended\Loader.php in favour of using sourcebroker/deployer-loader
c) [TASK][!!!BREAKING] Remove SourceBroker\DeployerExtended\Utility\FileUtility->requireFilesFromDirectoryReqursively
   because it was used only in SourceBroker\DeployerExtended\Loader.php

6.1.3
~~~~~

a) [BUGFIX] Fix problem when few request want to delete the same file in buffer tasks.
b) [TASK] Increase req for php to 5.6 as deployer does not work with php 5.4.

6.1.2
~~~~~

a) Fix missing changelog.

6.1.1
~~~~~

a) Fix hardcoded locker file name.
b) Docs update.

6.1.0
~~~~~

a) Add option to buffer:start to auto remove lock files after some time.
b) Add option "entrypoint_refresh"

6.0.0
~~~~~

a) Start entrypoint in task "buffer:start" and "buffer:stop" from deploy_path and not form web_path
b) Remove not used var "tmp_dir".

5.1.0
~~~~~

a) Rework of php:clear_cache_http. Look for old clear_cache file in previous release.

5.0.0
~~~~~

a) Remove autoload of recipes. From now an object of class Loader must be created that will load
   the recipes.

4.0.0
~~~~~

Tasks removed with replacement in other package: https://github.com/sourcebroker/deployer-extended-database

a) db:download
b) db:export
c) db:import
d) db:move
e) db:process
f) db:pull
g) db:truncate
h) db:upload

Tasks removed with replacement in other package: https://github.com/sourcebroker/deployer-extended-media

a) media:move
b) media:pull
c) media:push

3.0.0
~~~~~

Flatten structure of databases settings for database tasks.

Structure was:
::

 set(
       'db_databases',
       [
           ['database_foo' => [
                   'host' => '127.0.0.1',
                   'database' => 'foo',
                   'user' => 'foo',
                   'password' => 'foopass',
                  ]
           ],
           ['database_foo' => get('db_default')]
           ['database_bar' => [
                   'host' => '127.0.0.1',
                   'database' => 'bar',
                   'user' => 'bar',
                   'password' => 'barpass',
                  ],
           ],
           ['database_bar' => get('db_default')]
           ['database_bar' => '/absolute/path/to/file/with/config_array.php']
       ]
   );

Should be now:
::

 set(
       'db_databases',
       [
           'database_foo' => [
               [
                   'host' => '127.0.0.1',
                   'database' => 'foo',
                   'user' => 'foo',
                   'password' => 'foopass',
               ],
               get('db_default'),
               '/absolute/path/to/file/with/config_array.php'
           ],
           'database_bar' => [
               get('db_default'),
               '/absolute/path/to/file/with/config_array.php'
           ],
       ]
   );

All of the arrays in each database defined by key will be merged.

2.0.0
~~~~~

Task renamed:

a) Rename deploy:composer_check_install to ``deploy:check_composer_install``_
b) Rename cache:clearstatcache to ``php:clear_cache_cli``_
c) Rename cache:frontendreset to ``php:clear_cache_http``_
d) Rename deploy:vhosts to ``config:vhost``_

Task splitted/renamed with no simple replacement:

a) file:remove_recursive_atomic - replaced by ``file:rm2steps:1``_, ``file:rm2steps:2``_
b) lock:create_lock_files - replaced by ``buffer:start``_
c) lock:delete_lock_files - replaced by ``buffer:stop``_
d) lock:overwrite_entry_point - replaced by ``buffer:start``_

Task removed with no replacement:

a) file:copy_from_shared
b) file:copy_from_previous
c) git:check_status
d) lock:stop_if_http_status_200
