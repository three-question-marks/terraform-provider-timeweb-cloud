---
page_title: "twc_db_mysql_5 Resource - Timeweb Cloud"
subcategory: ""
description: |-
  Resource for describing needed MySQL 5.7 database and provides actual information about its status
---

# twc_db_mysql_5 (Resource)

Resource for describing needed MySQL 5.7 database and provides actual information about its status

## Примеры использования

```terraform
# Select any preset from location = "ru-1", 8 Gb disk space, for database type `mysql`, with price between 100 and 200 RUB
data "twc_db_preset" "example-db-preset" {
  location = "ru-1"

  disk = 8 * 1024
  type = "mysql"

  price_filter {
    from = 100
    to = 200
  }
}

# Example usage of MySQL 5.7 database resource
resource "twc_db_mysql_5" "example-mysql-5" {
  name = "example_mysql_5"

  login = "example_login"
  password = "example_password"

  preset_id = data.twc_db_preset.example-db-preset.id
}
```
<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `name` (String) Name for database
- `password` (String, Sensitive) Password for database
- `preset_id` (Number) Preset ID for database

### Optional

- `auto_increment_increment` (Number) Interval between indices between rows for `AUTO_INCREMENT` columns
- `auto_increment_offset` (Number) Start value for `AUTO_INCREMENT` columns
- `hash_type` (String) Hash type for database
- `innodb_io_capacity` (Number) IOPS count
- `innodb_purge_threads` (Number) Threads count for cleanup operation
- `innodb_read_io_threads` (Number) Threads count for read operation
- `innodb_thread_concurrency` (Number) Maximum active threads count
- `innodb_write_io_threads` (Number) Threads count for write operation
- `is_external_ip` (Boolean) Flag that shows allowability database only by external IP address
- `join_buffer_size` (String) Buffer size for JOIN operation
- `login` (String) Login for database
- `max_allowed_packet` (String) Max allowed size for one packet or parameter that may be sent via `mysql_stmt_send_long_data()`
- `max_heap_table_size` (String) Max size for user MEMORY-tables
- `project_id` (Number) Project ID for created DB

### Read-Only

- `disk_stats` (List of Object) Information about database disk stats (see [below for nested schema](#nestedatt--disk_stats))
- `host` (String) Host for connection to database
- `id` (String) The ID of this resource.
- `ip` (String) IP-address database of network interface
- `local_ip` (String) Local IP-address database of network interface
- `port` (Number) Port for connection to database
- `status` (String) Current status of database (`started`, `starting`, `stoped`, `no_paid`)

<a id="nestedatt--disk_stats"></a>
### Nested Schema for `disk_stats`

Read-Only:

- `size` (Number)
- `used` (Number)

## Import

Import is supported using the following syntax:

```shell
# Database can be imported by specifying the numeric identifier from URL
terraform import twc_db_mysql_5.example 42
```