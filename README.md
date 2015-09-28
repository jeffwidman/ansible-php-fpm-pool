php-fpm_pool
=========

This is an Ansible helper role for installing and managing multiple php-fpm
pools on servers setup using the [Centminmod](http://centminmod.com/) bash script.

If you're using Centminmod, the following roles play well together:
  - **[centminmod wrapper](https://github.com/jeffwidman/ansible-centminmod)** (handles basic install + tuning common configuration settings)
  - **[mariadb](https://github.com/jeffwidman/ansible-mariadb)** (configures common my.cnf settings)
  - **[centminmod-domain-verification](https://github.com/jeffwidman/ansible-centminmod-domain-verification)** (tests that individual domains are configured properly)
  - **[php-fpm-pool](https://github.com/jeffwidman/ansible-php-fpm-pool)** (for creating/managing individual php-fpm pools for each PHP app)

Example meta file:
----------------
To use this, in your domain-specific or app-specific role, add a meta dependency
and pass required variables.

Make sure that every pool on a given server has a unique `pool_tcp_port` number.

    ---
    # meta file for jeffwidman_com role

    dependencies:
      - { role: php-fpm-pool,
            pool_name: "{{ jeff_blog_phpfpm_pool_name }}",
            pool_tcp_port: 9002,
            pool_user: "{{ jeff_blog_linux_user }}",
            pool_group: "{{ jeff_blog_linux_user }}",
            pm_type: ondemand,
            pm_max_children: 6
            }

License
-------

MIT

Author Information
------------------

Jeff Widman jeff@jeffwidman.com
