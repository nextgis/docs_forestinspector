.. sectionauthor:: Дмитрий Барышников <dmitry.baryshnikov@nextgis.ru>

.. _ngfv_install:

Установка
=========


Используемые Python-пакеты
--------------------------

+ nextgisweb (ветка ``history``)
+ nextgisweb_mapserver
+ nextgisweb_lookuptable
+ nextgisweb_forest_violations


Поддержка истории
-----------------

Ветка ``history`` добавляет возможность сделать тот или иной векторный
слой отслеживаемым. Для этого используется расширение
``pghistory-tracker``, подробнее об его установке
`тут <https://github.com/nextgis/nextgisweb_forest_violations/wiki/History-Tracking>`_.


SELinux и nginx
---------------

При развертывании приложения с использованием uWSGI и nginx возникает
проблема, описанная в `статье <http://axilleas.me/en/blog/2013/selinux-policy-for-nginx-and-gitlab-unix-socket-in-fedora-19/>`_.
Для её решения скомпилируем и установим специальный модуль для SELinux:

.. code:: bash

    checkmodule -M -m -o nginx.mod nginx.te
    semodule_package -o nginx.pp -m nginx.mod
    semodule -i nginx.pp

Содержимое файла ``nginx.te``:

.. code:: bash

    module nginx 1.0;

    require {
        type var_run_t;
        type user_home_dir_t;
        type httpd_log_t;
        type httpd_t;
        type user_home_t;
        type unreserved_port_t;
        type httpd_sys_content_t;
        type initrc_t;
        type http_cache_port_t;
        class sock_file write;
        class unix_stream_socket connectto;
        class dir { search getattr };
        class file { read write setattr };
        class tcp_socket name_connect;
    }

    #============= httpd_t ==============

    #!!!! This avc can be allowed using one of the these booleans:
    #     nis_enabled, httpd_can_network_connect
    allow httpd_t unreserved_port_t:tcp_socket name_connect;

    #!!!! This avc is allowed in the current policy
    allow httpd_t http_cache_port_t:tcp_socket name_connect;
    allow httpd_t httpd_log_t:file setattr;
    allow httpd_t httpd_sys_content_t:sock_file write;
    allow httpd_t initrc_t:unix_stream_socket connectto;

    #!!!! This avc is allowed in the current policy
    allow httpd_t user_home_dir_t:dir search;

    #!!!! This avc is allowed in the current policy
    allow httpd_t user_home_t:dir { search getattr };
    allow httpd_t user_home_t:sock_file write;
    allow httpd_t var_run_t:file { read write };
