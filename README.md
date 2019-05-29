![](https://img.shields.io/badge/Ansible-graylog-green.svg?logo=angular&style=for-the-badge)

>__Please note that the original design goal of this role was more concerned with the initial installation and bootstrapping environment, which currently does not involve performing continuous maintenance, and therefore are only suitable for testing and development purposes,  should not be used in production environments.__

>__请注意，此角色的最初设计目标更关注初始安装和引导环境，目前不涉及执行连续维护，因此仅适用于测试和开发目的，不应在生产环境中使用。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_graylog.png" align="right" /></p>

__Table of Contents__

- [Overview](#overview)
- [Requirements](#requirements)
  * [Operating systems](#operating-systems)
  * [Graylog Versions](#graylog-versions)
- [ Role variables](#Role-variables)
  * [Main Configuration](#Main-parameters)
  * [Other Configuration](#Other-parameters)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Hosts inventory file](#Hosts-inventory-file)
  * [Vars in role configuration](#vars-in-role-configuration)
  * [Combination of group vars and playbook](#combination-of-group-vars-and-playbook)
- [License](#license)
- [Author Information](#author-information)
- [Contributors](#Contributors)

## Overview
This Ansible role installs Graylog on linux operating system, including establishing a filesystem structure and server configuration with some common operational features.

## Requirements
### Operating systems
This role will work on the following operating systems:

  * CentOS 7

### Graylog versions

The following list of supported the graylog releases:

  * Graylog 3.0

## Role variables
### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:

##### General parameters
* `graylog_cluster`: Cluster name of servers that implements distribution performance.
* `graylog_heap_size`: Specify the maximum memory allocation pool for a Java virtual machine.
* `graylog_path`: This directory is used to store Graylog server state.
* `graylog_root_email`: The email address of the root user.
* `graylog_root_password`: A SHA2 hash of a password for root user.
* `graylog_root_timezone`: The time zone setting of the root user.
* `graylog_root_username`: The default root username.
* `graylog_selinux`: SELinux security policy.
* `graylog_version`: Specify the Graylog version.
* `graylog_password_secret`: a secret that is used for password encryption and salting.

##### NGinx parameters
* `graylog_ngx_dept`: A boolean value, whether proxy web interface and API traffic using NGinx.
* `graylog_ngx_domain`: Defines domain name.
* `graylog_ngx_version`: extras or standard
* `graylog_ngx_port_http`: NGinx HTTP listen port.
* `graylog_ngx_port_https`: NGinx HTTPs listen port.
* `graylog_ngx_compress`: Enables or disables compression.
* `graylog_ngx_pagespeed`: Enables or disables pagespeed modules.
* `graylog_ngx_block_agents`: Enables or disables block unsafe User Agents.
* `graylog_ngx_block_string`: Enables or disables block includes Exploits / File injections / Spam / SQL injections.
* `graylog_ngx_ssl_protocols`: intermediate or modern, defines SSL protocol profile.

##### Elasticseach connection parameters
* `graylog_elastic_auth`: A boolean value, Enable or Disable Elasticsearch authentication.
* `graylog_elastic_cluster`: Specify name for your Elastic cluster name.
* `graylog_elastic_dept`: A boolean value, whether ElasticSearch use the same environment.
* `graylog_elastic_heap_size`: Specify the maximum memory allocation pool for a Java virtual machine.
* `graylog_elastic_hosts`: List of Elasticsearch hosts Graylog should connect to.
* `graylog_elastic_pass`: Elasticsearch authenticated password.
* `graylog_elastic_path`: Specify the ElasticSearch data directory.
* `graylog_elastic_port_rest`: Elasticsearch REST port.
* `graylog_elastic_user`: Elasticsearch authenticated user.
* `graylog_elastic_version`: Specify the Elasticsearch version.

##### MongoDB connection parameters
* `graylog_mongod_auth`: A boolean value, Enable or Disable MongoDB authentication.
* `graylog_mongod_dept`: A boolean value, whether MongoDB database use the same environment.
* `graylog_mongod_hosts`: Group of MongoDB hosts Graylog should connect to.
* `graylog_mongod_node_role`: Member role for ReplicaSet.
* `graylog_mongod_path`: Specify the MongoDB data directory.
* `graylog_mongod_pass`: MongoDB Graylog password.
* `graylog_mongod_port`: The MongoDB instance port.
* `graylog_mongod_replset`: MongoDB ReplicaSet name.
* `graylog_mongod_sa_pass`: MongoDB Superuser password.
* `graylog_mongod_sa_user`: MongoDB Superuser name.
* `graylog_mongod_user`: MongoDB Graylog username.
* `graylog_mongod_version`: Specify the MongoDB version, minimum 34.

##### Listen port
* `graylog_port_arg.api`: WEB / API network communication ports.

##### Service Mesh
* `environments`: Define the service environment.
* `consul_public_register`: Whether register a exporter service with public consul client.
* `consul_public_exporter_token`: Public Consul client ACL token.
* `consul_public_clients`: List of public consul clients.
* `consul_public_http_port`: The consul HTTP API port.

##### Email Variables
* `graylog_mail_arg.transport_email_enabled`: Enable mail for alert.
* `graylog_mail_arg.transport_email_hostname`: The SMTP host address.
* `graylog_mail_arg.transport_email_port`: The SMTP host communication port.
* `graylog_mail_arg.transport_email_use_auth`: Enable SMTP Authentication.
* `graylog_mail_arg.transport_email_use_tls`: Enable SMTP with STARTTLS for encrypted connections.
* `graylog_mail_arg.transport_email_use_ssl`: Enable SMTP over SSL (SMTPS) for encrypted connections.

##### System Variables
* `graylog_arg.alert_check_interval`: Length of the interval in seconds in which the alert conditions for all streams should be checked and alarms are being sent.
* `graylog_arg.allow_highlighting`: Allow searches to be highlighted.
* `graylog_arg.allow_leading_wildcard_searches`: Allow searches with leading wildcards.
* `graylog_arg.async_eventbus_processors`: Number of threads used exclusively for dispatching internal events.
* `graylog_arg.versionchecks`: Software version check
* `graylog_arg.disable_sigar`: Disable the use of SIGAR for collecting system stats.
* `graylog_arg.http_connect_timeout`: The default connect timeout for outgoing HTTP connections.
* `graylog_arg.http_enable_cors`: Enable CORS headers for HTTP interface.
* `graylog_arg.http_enable_gzip`: This compresses API responses and therefore helps to reduce overall round trip times.
* `graylog_arg.http_enable_tls`: Secures the communication with the HTTP interface with TLS.
* `graylog_arg.http_max_header_size`: The maximum size of the HTTP request headers in bytes.
* `graylog_arg.http_read_timeout`: The default read timeout for outgoing HTTP connections.
* `graylog_arg.http_thread_pool_size`: The size of the thread pool used exclusively for serving the HTTP interface.
* `graylog_arg.http_write_timeout`: The default write timeout for outgoing HTTP connections.
* `graylog_arg.index_ranges_cleanup_interval`: Time interval for index range information cleanups.
* `graylog_arg.inputbuffer_processors`: The number processors of input ring buffers.
* `graylog_arg.inputbuffer_ring_size`: Size of input ring buffers.
* `graylog_arg.inputbuffer_wait_strategy`: Wait strategy describing how buffer processors wait on a input sequence.
* `graylog_arg.message_journal_dir`: The directory which will be used to store the message journal.
* `graylog_arg.message_journal_enabled`: Enable the disk based message journal.
* `graylog_arg.message_journal_flush_age`: Specify a time interval at which we will force an fsync of data written to the log.
* `graylog_arg.message_journal_flush_interval`: Specify an interval at which we will force an fsync of data written to the log.
* `graylog_arg.message_journal_max_age`: The maximum hours for journal hold messages before they could be written.
* `graylog_arg.message_journal_max_size`: The maximum size for journal hold messages before they could be written.
* `graylog_arg.message_journal_segment_age`: Controls the period of time which Graylog will force the log to roll even
* `graylog_arg.message_journal_segment_size`: The segment size of message journal.
* `graylog_arg.mongod_max_connections`: The maximum connections your MongoDB server can handle from a single client.
* `graylog_arg.output_batch_size`: Batch size for the Elasticsearch output.
* `graylog_arg.output_flush_interval`: Flush interval (in seconds) for the Elasticsearch output.
* `graylog_arg.outputbuffer_processors`:Raise this number if your buffers are filling up.
* `graylog_arg.processbuffer_processors`: The number of parallel running processors.
* `graylog_arg.processor_wait_strategy`: Wait strategy describing how buffer processors wait on a cursor sequence
* `graylog_arg.ring_size`: Size of internal ring buffers.
* `graylog_arg.recvbuffer_sizes`: UDP receive buffer size for all message inputs.

##### Elasticsearch Variables
* `graylog_elastic_arg.compression_enabled`: Enable payload compression for Elasticsearch requests.
* `graylog_elastic_arg.connect_timeout`: Maximum amount of time to wait for successfull connection to Elasticsearch HTTP port.
* `graylog_elastic_arg.disable_index_optimization`: Disable the optimization of Elasticsearch indices after index cycling.
* `graylog_elastic_arg.disable_version_check`: Disable checking the version of Elasticsearch for being compatible with Graylog release.
* `graylog_elastic_arg.discovery_enabled`: Enable automatic Elasticsearch node discovery through Nodes Info.
* `graylog_elastic_arg.discovery_filter`: Filter for including/excluding Elasticsearch nodes to their custom attributes.
* `graylog_elastic_arg.discovery_frequency`: Frequency of the Elasticsearch node discovery.
* `graylog_elastic_arg.idle_timeout`: Maximum idle time for an Elasticsearch connection.
* `graylog_elastic_arg.index_optimization_jobs`: Maximum number of concurrently running index optimization jobs.
* `graylog_elastic_arg.index_optimization_timeout`: Global timeout for index optimization requests.
* `graylog_elastic_arg.max_docs_per_index`: Maximum number of documents in an Elasticsearch index before a new index is being created
* `graylog_elastic_arg.max_number_of_indices`: How many indices do you want to keep.
* `graylog_elastic_arg.max_retries`: Maximum number of times Graylog will retry failed requests to Elasticsearch.
* `graylog_elastic_arg.max_size_per_index`: Maximum size in bytes per Elasticsearch index on disk before a new index is being created.
* `graylog_elastic_arg.max_time_per_index`: Maximum time before a new Elasticsearch index is being created.
* `graylog_elastic_arg.max_total_connections`: Maximum number of total connections to Elasticsearch.
* `graylog_elastic_arg.max_total_connections_per_route`: Maximum number of total connections per Elasticsearch route.
* `graylog_elastic_arg.replicas`: The number of replicas for your indices.
* `graylog_elastic_arg.request_timeout`: Global request timeout for Elasticsearch requests.
* `graylog_elastic_arg.retention_strategy`: Decide what happens with the oldest indices when the maximum number of indices is reached.
* `graylog_elastic_arg.rotation_strategy`: The strategy it uses to determine when to rotate the currently active write index.
* `graylog_elastic_arg.shards`: The number of shards for your indices.
* `graylog_elastic_arg.socket_timeout`: Maximum amount of time to wait for reading back a response from an Elasticsearch server.

##### Inputs Variables
* `graylog_inputs_arg`: Define the global inputs parameters.

##### Content Packs Variables
* `graylog_content_packs_arg`: Define the Content Packs parameters.

##### Indexes Optimization Tuning
* `graylog_indexes_arg`: Define the customer index parameters.

### Other parameters
There are some variables in vars/main.yml:
* `graylog_kernel_parameters`: Operating system variables.

## Dependencies
- Ansible versions > 2.6 are supported.
- [NGinx](https://github.com/goldstrike77/ansible-role-linux-nginx.git)
- [MongoDB](https://github.com/goldstrike77/ansible-role-linux-mongodb.git) 
- [Elasticsearch](https://github.com/goldstrike77/ansible-role-linux-elasticsearch.git)

## Example

### Hosts inventory file
See tests/inventory for an example.

    node01 ansible_host='192.168.1.10' graylog_is_install='true' graylog_cluster='syslog'
    node02 ansible_host='192.168.1.11' graylog_is_install='true' graylog_cluster='syslog'
    node03 ansible_host='192.168.1.12' graylog_is_install='true' graylog_cluster='syslog'

### Vars in role configuration
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - role: ansible-role-linux-graylog
           graylog_is_install: true

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`

    graylog_is_install: true
    graylog_cluster: 'default'
    graylog_heap_size: '2G'
    graylog_path: '/data'
    graylog_root_email: 'somebody@domain.com'
    graylog_root_password: 'password'
    graylog_root_timezone: 'Asia/Shanghai'
    graylog_root_username: 'admin'
    graylog_selinux: 'false'
    graylog_version: '3.0'
    graylog_password_secret: 'yEgvvXw0XsRJrMrtfA6oLUpIWoD38kVJtYrknhNsxhkEEMa8AfxPhebUmKQMoQ9wXQwp2jZQMbPHjjMFMjBMcBMyaKFBVcap'
    graylog_ngx_dept: false
    graylog_ngx_block_agents: false
    graylog_ngx_block_string: false
    graylog_ngx_compress: false
    graylog_ngx_domain: 'syslog.example.com'
    graylog_ngx_pagespeed: false
    graylog_ngx_port_http: '80'
    graylog_ngx_port_https: '443'
    graylog_ngx_ssl_protocols: 'modern'
    graylog_ngx_version: 'extras'
    graylog_elastic_auth: false
    graylog_elastic_cluster: 'graylog'
    graylog_elastic_dept: false
    graylog_elastic_hosts: 'localhost'
    graylog_elastic_heap_size: '3g'
    graylog_elastic_pass: 'password'
    graylog_elastic_path: '/data'
    graylog_elastic_port_rest: '9200'
    graylog_elastic_user: 'elastic'
    graylog_elastic_version: '5.6.16'
    graylog_mongod_auth: false
    graylog_mongod_dept: false
    graylog_mongod_hosts: 'localhost'
    graylog_mongod_node_role: 'replica'
    graylog_mongod_path: '/data'
    graylog_mongod_pass: 'password'
    graylog_mongod_port: '27017'
    graylog_mongod_replset: 'graylog'
    graylog_mongod_sa_pass: 'password'
    graylog_mongod_sa_user: 'sa'
    graylog_mongod_user: 'graylog'
    graylog_mongod_version: '36'
    graylog_port_arg:
      api: '9099'
    graylog_mail_arg:
      transport_email_enabled: false
      transport_email_hostname: 'localhost'
      transport_email_port: '25'
      transport_email_use_auth: false
      transport_email_use_tls: false
      transport_email_use_ssl: false
    graylog_arg:
      alert_check_interval: '60'
      allow_highlighting: false
      allow_leading_wildcard_searches: false
      async_eventbus_processors: '2'
      versionchecks: false
      disable_sigar: true
      http_connect_timeout: '10s'
      http_enable_cors: true
      http_enable_gzip: true
      http_enable_tls: false
      http_max_header_size: '8192'
      http_read_timeout: '20s'
      http_thread_pool_size: '12'
      http_write_timeout: '20s'
      index_ranges_cleanup_interval: '1h'
      inputbuffer_processors: '2'
      inputbuffer_ring_size: '65536'
      inputbuffer_wait_strategy: 'blocking'
      message_journal_dir: '{{ graylog_path }}/graylog/journal'
      message_journal_enabled: true
      message_journal_flush_age: '1m'
      message_journal_flush_interval: '1000000'
      message_journal_max_age: '12h'
      message_journal_max_size: '10gb'
      message_journal_segment_age: '1h'
      message_journal_segment_size: '200mb'
      mongod_max_connections: '1000'
      output_batch_size: '500'
      output_flush_interval: '1'
      outputbuffer_processors: '2'
      processbuffer_processors: '2'
      processor_wait_strategy: 'blocking'
      ring_size: '65536'
      recvbuffer_sizes: '2097152'
    graylog_elastic_arg:
      compression_enabled: true
      connect_timeout: '10s'
      disable_index_optimization: false
      disable_version_check: true
      discovery_enabled: false
      discovery_filter: ''
      discovery_frequency: '30s'
      idle_timeout: '600s'
      index_optimization_jobs: '20'
      index_optimization_timeout: '1h'
      max_docs_per_index: '20000000'
      max_number_of_indices: '20'
      max_retries: '3'
      max_size_per_index: '1073741824'
      max_time_per_index: '1d'
      max_total_connections: '20'
      max_total_connections_per_route: '3'
      replicas: '0'
      request_timeout: '1m'
      retention_strategy: 'delete'
      rotation_strategy: 'count'
      shards: '1'
      socket_timeout: '60s'
    graylog_inputs_arg:
      - name: 'GELF UDP'
        type: 'org.graylog2.inputs.gelf.udp.GELFUDPInput'
        port: 12201
      - name: 'Syslog UDP'
        type: 'org.graylog2.inputs.syslog.udp.SyslogUDPInput'
        port: 1514
      - name: 'CEF UDP Input'
        type: 'org.graylog.plugins.cef.input.CEFUDPInput'
        port: 5555
        graylog_indexes_arg:
    graylog_content_packs_arg:
      - name: 'NGinx'
        protocol: 'udp'
        port: '12302-12301'
    graylog_indexes_arg:
      - refresh_interval: '30s'
        translog:
          sync_interval: '30s'
          durability: 'async'
    environments: 'SIT'
    consul_public_register: false
    consul_public_exporter_token: '00000000-0000-0000-0000-000000000000'
    consul_public_clients: 'localhost'
    consul_public_http_port: '8500'

## License
![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## Author Information
Please send your suggestions to make this role better.

## Contributors
Special thanks to the [Connext Information Technology](http://www.connext.com.cn) for their contributions to this role.