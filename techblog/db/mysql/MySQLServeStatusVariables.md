# MySQL性能参数汇总

在MySQL中可以使用`SHOW STATUS`语句来查看MySQL数据库的性能参数，我们可以根据这些性能参数来了解MySQL数据库的状态，并制定合理的优化策略。

执行`show status;`可以查看所有的性能参数，执行`show status like '参数名称';`可以查看指定参数名称的性能参数，一般某一类参数都有相同的前缀。

## 翻译整理

<table cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td>
<p><strong>状态名</strong></p>
</td>
<td>
<p><strong>作用域</strong></p>
</td>
<td>
<p><strong>详细解释</strong></p>
</td>
</tr>
<tr>
<td>
<p>Aborted_clients</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>由于客户端没有正确关闭连接导致客户端终止而中断的连接数</p>
</td>
</tr>
<tr>
<td>
<p>Aborted_connects</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>试图连接到MySQL服务器而失败的连接数</p>
</td>
</tr>
<tr>
<td>
<p>Binlog_cache_disk_use</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>使用临时二进制日志缓存但超过binlog_cache_size值并使用临时文件来保存事务中的语句的事务数量</p>
</td>
</tr>
<tr>
<td>
<p>Binlog_cache_use</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>使用临时二进制日志缓存的事务数量</p>
</td>
</tr>
<tr>
<td>
<p>Bytes_received</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>从所有客户端接收到的字节数。</p>
</td>
</tr>
<tr>
<td>
<p>Bytes_sent</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>发送给所有客户端的字节数。</p>
</td>
</tr>
<tr>
<td>
<p>com*</p>
</td>
<td>
<p>&nbsp;</p>
</td>
<td>
<p>各种数据库操作的数量</p>
</td>
</tr>
<tr>
<td>
<p>Compression</p>
</td>
<td>
<p>Session</p>
</td>
<td>
<p>客户端与服务器之间只否启用压缩协议</p>
</td>
</tr>
<tr>
<td>
<p>Connections</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>试图连接到(不管是否成功)MySQL服务器的连接数</p>
</td>
</tr>
<tr>
<td>
<p>Created_tmp_disk_tables</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>服务器执行语句时在硬盘上自动创建的临时表的数量</p>
</td>
</tr>
<tr>
<td>
<p>Created_tmp_files</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>mysqld已经创建的临时文件的数量</p>
</td>
</tr>
<tr>
<td>
<p>Created_tmp_tables</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>服务器执行语句时自动创建的内存中的临时表的数量。如果Created_tmp_disk_tables较大，你可能要增加tmp_table_size值使临时&nbsp;表基于内存而不基于硬盘</p>
</td>
</tr>
<tr>
<td>
<p>Delayed_errors</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>用INSERT DELAYED写的出现错误的行数(可能为duplicate key)。</p>
</td>
</tr>
<tr>
<td>
<p>Delayed_insert_threads</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>使用的INSERT DELAYED处理器线程数。</p>
</td>
</tr>
<tr>
<td>
<p>Delayed_writes</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>写入的INSERT DELAYED行数</p>
</td>
</tr>
<tr>
<td>
<p>Flush_commands</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>执行的FLUSH语句数。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_commit</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>内部提交语句数</p>
</td>
</tr>
<tr>
<td>
<p>Handler_delete</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>行从表中删除的次数。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_discover</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>MySQL服务器可以问NDB CLUSTER存储引擎是否知道某一名字的表。这被称作发现。Handler_discover说明通过该方法发现的次数。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_prepare</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>A counter for the prepare phase of two-phase commit operations.</p>
</td>
</tr>
<tr>
<td>
<p>Handler_read_first</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>索引中第一条被读的次数。如果较高，它建议服务器正执行大量全索引扫描；例如，SELECT col1 FROM foo，假定col1有索引。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_read_key</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>根据键读一行的请求数。如果较高，说明查询和表的索引正确。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_read_next</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>按照键顺序读下一行的请求数。如果你用范围约束或如果执行索引扫描来查询索引列，该值增加。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_read_prev</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>按照键顺序读前一行的请求数。该读方法主要用于优化ORDER BY ... DESC。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_read_rnd</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>根据固定位置读一行的请求数。如果你正执行大量查询并需要对结果进行排序该值较高。你可能使用了大量需要MySQL扫描整个表的查询或你的连接没有正确使用键。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_read_rnd_next</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在数据文件中读下一行的请求数。如果你正进行大量的表扫描，该值较高。通常说明你的表索引不正确或写入的查询没有利用索引。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_rollback</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>内部ROLLBACK语句的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_savepoint</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在一个存储引擎放置一个保存点的请求数量。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_savepoint_rollback</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在一个存储引擎的要求回滚到一个保存点数目。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_update</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在表内更新一行的请求数。</p>
</td>
</tr>
<tr>
<td>
<p>Handler_write</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在表内插入一行的请求数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_buffer_pool_pages_data</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>包含数据的页数(脏或干净)。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_buffer_pool_pages_dirty</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>当前的脏页数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_buffer_pool_pages_flushed</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>要求清空的缓冲池页数</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_buffer_pool_pages_free</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>空页数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_buffer_pool_pages_latched</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>在InnoDB缓冲池中锁定的页数。这是当前正读或写或由于其它原因不能清空或删除的页数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_buffer_pool_pages_misc</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>忙的页数，因为它们已经被分配优先用作管理，例如行锁定或适用的哈希索引。该值还可以计算为Innodb_buffer_pool_pages_total - Innodb_buffer_pool_pages_free - Innodb_buffer_pool_pages_data。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_buffer_pool_pages_total</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>缓冲池总大小（页数）。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_buffer_pool_read_ahead_rnd</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>InnoDB初始化的“随机”read-aheads数。当查询以随机顺序扫描表的一大部分时发生。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_buffer_pool_read_ahead_seq</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>InnoDB初始化的顺序read-aheads数。当InnoDB执行顺序全表扫描时发生。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_buffer_pool_read_requests</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>InnoDB已经完成的逻辑读请求数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_buffer_pool_reads</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>不能满足InnoDB必须单页读取的缓冲池中的逻辑读数量。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_buffer_pool_wait_free</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>一般情况，通过后台向InnoDB缓冲池写。但是，如果需要读或创建页，并且没有干净的页可用，则它还需要先等待页面清空。该计数器对等待实例进行记数。如果已经适当设置缓冲池大小，该值应小。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_buffer_pool_write_requests</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>向InnoDB缓冲池的写数量。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_data_fsyncs</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>fsync()操作数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_data_pending_fsyncs</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>当前挂起的fsync()操作数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_data_pending_reads</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>当前挂起的读数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_data_pending_writes</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>当前挂起的写数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_data_read</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>至此已经读取的数据数量（字节）。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_data_reads</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>数据读总数量。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_data_writes</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>数据写总数量。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_data_written</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>至此已经写入的数据量（字节）。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_dblwr_pages_written</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>已经执行的双写操作数量</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_dblwr_writes</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>双写操作已经写好的页数</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_log_waits</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>我们必须等待的时间，因为日志缓冲区太小，我们在继续前必须先等待对它清空</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_log_write_requests</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>日志写请求数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_log_writes</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>向日志文件的物理写数量。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_os_log_fsyncs</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>向日志文件完成的fsync()写数量。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_os_log_pending_fsyncs</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>挂起的日志文件fsync()操作数量。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_os_log_pending_writes</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>挂起的日志文件写操作</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_os_log_written</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>写入日志文件的字节数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_page_size</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>编译的InnoDB页大小(默认16KB)。许多值用页来记数；页的大小很容易转换为字节。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_pages_created</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>创建的页数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_pages_read</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>读取的页数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_pages_written</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>写入的页数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_row_lock_current_waits</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>当前等待的待锁定的行数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_row_lock_time</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>行锁定花费的总时间，单位毫秒。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_row_lock_time_avg</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>行锁定的平均时间，单位毫秒。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_row_lock_time_max</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>行锁定的最长时间，单位毫秒。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_row_lock_waits</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>一行锁定必须等待的时间数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_rows_deleted</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>从InnoDB表删除的行数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_rows_inserted</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>插入到InnoDB表的行数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_rows_read</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>从InnoDB表读取的行数。</p>
</td>
</tr>
<tr>
<td>
<p>Innodb_rows_updated</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>InnoDB表内更新的行数。</p>
</td>
</tr>
<tr>
<td>
<p>Key_blocks_not_flushed</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>键缓存内已经更改但还没有清空到硬盘上的键的数据块数量。</p>
</td>
</tr>
<tr>
<td>
<p>Key_blocks_unused</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>键缓存内未使用的块数量。你可以使用该值来确定使用了多少键缓存</p>
</td>
</tr>
<tr>
<td>
<p>Key_blocks_used</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>键缓存内使用的块数量。该值为高水平线标记，说明已经同时最多使用了多少块。</p>
</td>
</tr>
<tr>
<td>
<p>Key_read_requests</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>从缓存读键的数据块的请求数。</p>
</td>
</tr>
<tr>
<td>
<p>Key_reads</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>从硬盘读取键的数据块的次数。如果Key_reads较大，则Key_buffer_size值可能太小。可以用Key_reads/Key_read_requests计算缓存损失率。</p>
</td>
</tr>
<tr>
<td>
<p>Key_write_requests</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>将键的数据块写入缓存的请求数。</p>
</td>
</tr>
<tr>
<td>
<p>Key_writes</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>向硬盘写入将键的数据块的物理写操作的次数。</p>
</td>
</tr>
<tr>
<td>
<p>Last_query_cost</p>
</td>
<td>
<p>Session</p>
</td>
<td>
<p>用查询优化器计算的最后编译的查询的总成本。用于对比同一查询的不同查询方案的成本。默认值0表示还没有编译查询。&nbsp;默认值是0。Last_query_cost具有会话范围。</p>
</td>
</tr>
<tr>
<td>
<p>Max_used_connections</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>服务器启动后已经同时使用的连接的最大数量。</p>
</td>
</tr>
<tr>
<td>
<p>ndb*</p>
</td>
<td>
<p>&nbsp;</p>
</td>
<td>
<p>ndb集群相关</p>
</td>
</tr>
<tr>
<td>
<p>Not_flushed_delayed_rows</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>等待写入INSERT DELAY队列的行数。</p>
<p>&nbsp;</p>
</td>
</tr>
<tr>
<td>
<p>Open_files</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>打开的文件的数目。</p>
</td>
</tr>
<tr>
<td>
<p>Open_streams</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>打开的流的数量(主要用于记录)。</p>
</td>
</tr>
<tr>
<td>
<p>Open_table_definitions</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>缓存的.frm文件数量</p>
</td>
</tr>
<tr>
<td>
<p>Open_tables</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>当前打开的表的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Opened_files</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>文件打开的数量。不包括诸如套接字或管道其他类型的文件。&nbsp;也不包括存储引擎用来做自己的内部功能的文件。</p>
</td>
</tr>
<tr>
<td>
<p>Opened_table_definitions</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>已经缓存的.frm文件数量</p>
</td>
</tr>
<tr>
<td>
<p>Opened_tables</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>已经打开的表的数量。如果Opened_tables较大，table_cache&nbsp;值可能太小。</p>
</td>
</tr>
<tr>
<td>
<p>Prepared_stmt_count</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>当前的预处理语句的数量。&nbsp;(最大数为系统变量: max_prepared_stmt_count)&nbsp;</p>
</td>
</tr>
<tr>
<td>
<p>Qcache_free_blocks</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>查询缓存内自由内存块的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Qcache_free_memory</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>用于查询缓存的自由内存的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Qcache_hits</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>查询缓存被访问的次数。</p>
</td>
</tr>
<tr>
<td>
<p>Qcache_inserts</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>加入到缓存的查询数量。</p>
</td>
</tr>
<tr>
<td>
<p>Qcache_lowmem_prunes</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>由于内存较少从缓存删除的查询数量。</p>
</td>
</tr>
<tr>
<td>
<p>Qcache_not_cached</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>非缓存查询数(不可缓存，或由于query_cache_type设定值未缓存)。</p>
</td>
</tr>
<tr>
<td>
<p>Qcache_queries_in_cache</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>登记到缓存内的查询的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Qcache_total_blocks</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>查询缓存内的总块数。</p>
</td>
</tr>
<tr>
<td>
<p>Queries</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>服务器执行的请求个数，包含存储过程中的请求。</p>
</td>
</tr>
<tr>
<td>
<p>Questions</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>已经发送给服务器的查询的个数。</p>
</td>
</tr>
<tr>
<td>
<p>Rpl_status</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>失败安全复制状态(还未使用)。</p>
</td>
</tr>
<tr>
<td>
<p>Select_full_join</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>没有使用索引的联接的数量。如果该值不为0,你应仔细检查表的索引</p>
</td>
</tr>
<tr>
<td>
<p>Select_full_range_join</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在引用的表中使用范围搜索的联接的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Select_range</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在第一个表中使用范围的联接的数量。一般情况不是关键问题，即使该值相当大。</p>
</td>
</tr>
<tr>
<td>
<p>Select_range_check</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在每一行数据后对键值进行检查的不带键值的联接的数量。如果不为0，你应仔细检查表的索引。</p>
</td>
</tr>
<tr>
<td>
<p>Select_scan</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>对第一个表进行完全扫描的联接的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Slave_heartbeat_period</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>复制的心跳间隔</p>
</td>
</tr>
<tr>
<td>
<p>Slave_open_temp_tables</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>从服务器打开的临时表数量</p>
</td>
</tr>
<tr>
<td>
<p>Slave_received_heartbeats</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>从服务器心跳数</p>
</td>
</tr>
<tr>
<td>
<p>Slave_retried_transactions</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>本次启动以来从服务器复制线程重试次数</p>
</td>
</tr>
<tr>
<td>
<p>Slave_running</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>如果该服务器是连接到主服务器的从服务器，则该值为ON。</p>
</td>
</tr>
<tr>
<td>
<p>Slow_launch_threads</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>创建时间超过slow_launch_time秒的线程数。</p>
</td>
</tr>
<tr>
<td>
<p>Slow_queries</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>查询时间超过long_query_time秒的查询的个数。</p>
</td>
</tr>
<tr>
<td>
<p>Sort_merge_passes</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>排序算法已经执行的合并的数量。如果这个变量值较大，应考虑增加sort_buffer_size系统变量的值。</p>
</td>
</tr>
<tr>
<td>
<p>Sort_range</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>在范围内执行的排序的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Sort_rows</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>已经排序的行数。</p>
</td>
</tr>
<tr>
<td>
<p>Sort_scan</p>
</td>
<td>
<p>Both</p>
</td>
<td>
<p>通过扫描表完成的排序的数量。</p>
</td>
</tr>
<tr>
<td>
<p>ssl＊</p>
</td>
<td>
<p>&nbsp;</p>
</td>
<td>
<p>ssl连接相关</p>
</td>
</tr>
<tr>
<td>
<p>Table_locks_immediate</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>立即获得的表的锁的次数。</p>
</td>
</tr>
<tr>
<td>
<p>Table_locks_waited</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>不能立即获得的表的锁的次数。如果该值较高，并且有性能问题，你应首先优化查询，然后拆分表或使用复制。</p>
</td>
</tr>
<tr>
<td>
<p>Threads_cached</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>线程缓存内的线程的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Threads_connected</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>当前打开的连接的数量。</p>
</td>
</tr>
<tr>
<td>
<p>Threads_created</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>创建用来处理连接的线程数。如果Threads_created较大，你可能要增加thread_cache_size值。缓存访问率的计算方法Threads_created/Connections。</p>
</td>
</tr>
<tr>
<td>
<p>Threads_running</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>激活的（非睡眠状态）线程数。</p>
</td>
</tr>
<tr>
<td>
<p>Uptime</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>服务器已经运行的时间（以秒为单位）。</p>
</td>
</tr>
<tr>
<td>
<p>Uptime_since_flush_status</p>
</td>
<td>
<p>Global</p>
</td>
<td>
<p>最近一次使用FLUSH STATUS&nbsp;的时间（以秒为单位）。</p>
</td>
</tr>
</tbody>
</table>

## 官方文档

[MySQL Server Status Variables](https://dev.mysql.com/doc/refman/8.0/en/server-status-variables.html)

The MySQL server maintains many status variables that provide information about its operation. You can view these variables and their values by using the SHOW [GLOBAL | SESSION] STATUS statement (see Section 13.7.6.35, “SHOW STATUS Syntax”). The optional GLOBAL keyword aggregates the values over all connections, and SESSION shows the values for the current connection.

```sql
mysql> SHOW GLOBAL STATUS;
+-----------------------------------+------------+
| Variable_name                     | Value      |
+-----------------------------------+------------+
| Aborted_clients                   | 0          |
| Aborted_connects                  | 0          |
| Bytes_received                    | 155372598  |
| Bytes_sent                        | 1176560426 |
...
| Connections                       | 30023      |
| Created_tmp_disk_tables           | 0          |
| Created_tmp_files                 | 3          |
| Created_tmp_tables                | 2          |
...
| Threads_created                   | 217        |
| Threads_running                   | 88         |
| Uptime                            | 1389872    |
+-----------------------------------+------------+
```

Many status variables are reset to 0 by the FLUSH STATUS statement.

This section provides a description of each status variable. For a status variable summary, see Section 5.1.6, “Server Status Variable Reference”.

The status variables have the following meanings.

Aborted_clients

The number of connections that were aborted because the client died without closing the connection properly. See Section B.4.2.10, “Communication Errors and Aborted Connections”.

Aborted_connects

The number of failed attempts to connect to the MySQL server. See Section B.4.2.10, “Communication Errors and Aborted Connections”.

For additional connection-related information, check the Connection_errors_xxx status variables and the host_cache table.

Binlog_cache_disk_use

The number of transactions that used the temporary binary log cache but that exceeded the value of binlog_cache_size and used a temporary file to store statements from the transaction.

The number of nontransactional statements that caused the binary log transaction cache to be written to disk is tracked separately in the Binlog_stmt_cache_disk_use status variable.

Acl_cache_items_count

The number of cached privilege objects. Each object is the privilege combination of a user and its active roles.

Binlog_cache_use

The number of transactions that used the binary log cache.

Binlog_stmt_cache_disk_use

The number of nontransaction statements that used the binary log statement cache but that exceeded the value of binlog_stmt_cache_size and used a temporary file to store those statements.

Binlog_stmt_cache_use

The number of nontransactional statements that used the binary log statement cache.

Bytes_received

The number of bytes received from all clients.

Bytes_sent

The number of bytes sent to all clients.

Caching_sha2_password_rsa_public_key

The public key used by the caching_sha2_password authentication plugin for RSA key pair-based password exchange. The value is nonempty only if the server successfully initializes the private and public keys in the files named by the caching_sha2_password_private_key_path and caching_sha2_password_public_key_path system variables. The value of Caching_sha2_password_rsa_public_key comes from the latter file.

Com_xxx

The Com_xxx statement counter variables indicate the number of times each xxx statement has been executed. There is one status variable for each type of statement. For example, Com_delete and Com_update count DELETE and UPDATE statements, respectively. Com_delete_multi and Com_update_multi are similar but apply to DELETE and UPDATE statements that use multiple-table syntax.

The discussion at the beginning of this section indicates how to relate these statement-counting status variables to other such variables.

All of the Com_stmt_xxx variables are increased even if a prepared statement argument is unknown or an error occurred during execution. In other words, their values correspond to the number of requests issued, not to the number of requests successfully completed.

The Com_stmt_xxx status variables are as follows:

Com_stmt_prepare

Com_stmt_execute

Com_stmt_fetch

Com_stmt_send_long_data

Com_stmt_reset

Com_stmt_close

Those variables stand for prepared statement commands. Their names refer to the COM_xxx command set used in the network layer. In other words, their values increase whenever prepared statement API calls such as mysql_stmt_prepare(), mysql_stmt_execute(), and so forth are executed. However, Com_stmt_prepare, Com_stmt_execute and Com_stmt_close also increase for PREPARE, EXECUTE, or DEALLOCATE PREPARE, respectively. Additionally, the values of the older statement counter variables Com_prepare_sql, Com_execute_sql, and Com_dealloc_sql increase for the PREPARE, EXECUTE, and DEALLOCATE PREPARE statements. Com_stmt_fetch stands for the total number of network round-trips issued when fetching from cursors.

Com_stmt_reprepare indicates the number of times statements were automatically reprepared by the server, for example, after metadata changes to tables or views referred to by the statement. A reprepare operation increments Com_stmt_reprepare, and also Com_stmt_prepare.

Com_explain_other indicates the number of EXPLAIN FOR CONNECTION statements executed. See Section 8.8.4, “Obtaining Execution Plan Information for a Named Connection”.

Com_change_repl_filter indicates the number of CHANGE REPLICATION FILTER statements executed.

Compression

Whether the client connection uses compression in the client/server protocol.

As of MySQL 8.0.18, this status variable is deprecated. It will be removed in a future MySQL version. See Legacy Connection Compression Configuration.

Compression_algorithm

The name of the compression algorithm in use for the current connection to the server. The value can be any algorithm permitted in the value of the protocol_compression_algorithms system variable. For example, the value is uncompressed if the connection does not use compression, or zlib if the connection uses the zlib algorithm.

For more information, see Section 4.2.6, “Connection Compression Control”.

This variable was added in MySQL 8.0.18.

Compression_level

The compression level in use for the current connection to the server. The value is 6 for zlib connections (the default zlib algorithm compression level), 1 to 22 for zstd connections, and 0 for uncompressed connections.

For more information, see Section 4.2.6, “Connection Compression Control”.

This variable was added in MySQL 8.0.18.

Connection_errors_xxx

These variables provide information about errors that occur during the client connection process. They are global only and represent error counts aggregated across connections from all hosts. These variables track errors not accounted for by the host cache (see Section 8.12.4.2, “DNS Lookup Optimization and the Host Cache”), such as errors that are not associated with TCP connections, occur very early in the connection process (even before an IP address is known), or are not specific to any particular IP address (such as out-of-memory conditions).

Connection_errors_accept

The number of errors that occurred during calls to accept() on the listening port.

Connection_errors_internal

The number of connections refused due to internal errors in the server, such as failure to start a new thread or an out-of-memory condition.

Connection_errors_max_connections

The number of connections refused because the server max_connections limit was reached.

Connection_errors_peer_address

The number of errors that occurred while searching for connecting client IP addresses.

Connection_errors_select

The number of errors that occurred during calls to select() or poll() on the listening port. (Failure of this operation does not necessarily means a client connection was rejected.)

Connection_errors_tcpwrap

The number of connections refused by the libwrap library.

Connections

The number of connection attempts (successful or not) to the MySQL server.

Created_tmp_disk_tables

The number of internal on-disk temporary tables created by the server while executing statements.

If an internal temporary table is created initially as an in-memory table but becomes too large, MySQL automatically converts it to an on-disk table. The maximum size for in-memory temporary tables is the minimum of the tmp_table_size and max_heap_table_size values. If Created_tmp_disk_tables is large, you may want to increase the tmp_table_size or max_heap_table_size value to lessen the likelihood that internal temporary tables in memory will be converted to on-disk tables.

You can compare the number of internal on-disk temporary tables created to the total number of internal temporary tables created by comparing the values of the Created_tmp_disk_tables and Created_tmp_tables variables.

See also Section 8.4.4, “Internal Temporary Table Use in MySQL”.

Created_tmp_files

How many temporary files mysqld has created.

Created_tmp_tables

The number of internal temporary tables created by the server while executing statements.

You can compare the number of internal on-disk temporary tables created to the total number of internal temporary tables created by comparing the values of the Created_tmp_disk_tables and Created_tmp_tables variables.

See also Section 8.4.4, “Internal Temporary Table Use in MySQL”.

Each invocation of the SHOW STATUS statement uses an internal temporary table and increments the global Created_tmp_tables value.

Current_tls_ca

The active ssl_ca value in the SSL context that the server uses for new connections. This context value may differ from the current ssl_ca system variable value if the system variable has been changed but ALTER INSTANCE RELOAD TLS has not subsequently been executed to reconfigure the SSL context from the context-related system variable values and update the corresponding status variables. (This potential difference in values applies to each corresponding pair of context-related system and status variables. See Server-Side Runtime Configuration for Encrypted Connections.)

This variable was added in MySQL 8.0.16.

Current_tls_capath

The active ssl_capath value in the SSL context that the server uses for new connections. For notes about the relationship between this status variable and its corresponding system variable, see the description of Current_tls_ca.

This variable was added in MySQL 8.0.16.

Current_tls_cert

The active ssl_cert value in the SSL context that the server uses for new connections. For notes about the relationship between this status variable and its corresponding system variable, see the description of Current_tls_ca.

This variable was added in MySQL 8.0.16.

Current_tls_cipher

The active ssl_cipher value in the SSL context that the server uses for new connections. For notes about the relationship between this status variable and its corresponding system variable, see the description of Current_tls_ca.

This variable was added in MySQL 8.0.16.

Current_tls_ciphersuites

The active tls_ciphersuites value in the SSL context that the server uses for new connections. For notes about the relationship between this status variable and its corresponding system variable, see the description of Current_tls_ca.

This variable was added in MySQL 8.0.16.

Current_tls_crl

The active ssl_crl value in the SSL context that the server uses for new connections. For notes about the relationship between this status variable and its corresponding system variable, see the description of Current_tls_ca.

This variable was added in MySQL 8.0.16.

Current_tls_crlpath

The active ssl_crlpath value in the SSL context that the server uses for new connections. For notes about the relationship between this status variable and its corresponding system variable, see the description of Current_tls_ca.

This variable was added in MySQL 8.0.16.

Current_tls_key

The active ssl_key value in the SSL context that the server uses for new connections. For notes about the relationship between this status variable and its corresponding system variable, see the description of Current_tls_ca.

This variable was added in MySQL 8.0.16.

Current_tls_version

The active tls_version value in the SSL context that the server uses for new connections. For notes about the relationship between this status variable and its corresponding system variable, see the description of Current_tls_ca.

This variable was added in MySQL 8.0.16.

Delayed_errors

This status variable is deprecated (because DELAYED inserts are not supported), and will be removed in a future release.

Delayed_insert_threads

This status variable is deprecated (because DELAYED inserts are not supported), and will be removed in a future release.

Delayed_writes

This status variable is deprecated (because DELAYED inserts are not supported), and will be removed in a future release.

dragnet.Status

The result of the most recent assignment to the dragnet.log_error_filter_rules system variable, empty if no such assignment has occurred.

This variable was added in MySQL 8.0.12.

Flush_commands

The number of times the server flushes tables, whether because a user executed a FLUSH TABLES statement or due to internal server operation. It is also incremented by receipt of a COM_REFRESH packet. This is in contrast to Com_flush, which indicates how many FLUSH statements have been executed, whether FLUSH TABLES, FLUSH LOGS, and so forth.

group_replication_primary_member

Shows the primary member's UUID when the group is operating in single-primary mode. If the group is operating in multi-primary mode, shows an empty string.

The group_replication_primary_member status variable has been deprecated and is scheduled to be removed in a future version.

Handler_commit

The number of internal COMMIT statements.

Handler_delete

The number of times that rows have been deleted from tables.

Handler_external_lock

The server increments this variable for each call to its external_lock() function, which generally occurs at the beginning and end of access to a table instance. There might be differences among storage engines. This variable can be used, for example, to discover for a statement that accesses a partitioned table how many partitions were pruned before locking occurred: Check how much the counter increased for the statement, subtract 2 (2 calls for the table itself), then divide by 2 to get the number of partitions locked.

Handler_mrr_init

The number of times the server uses a storage engine's own Multi-Range Read implementation for table access.

Handler_prepare

A counter for the prepare phase of two-phase commit operations.

Handler_read_first

The number of times the first entry in an index was read. If this value is high, it suggests that the server is doing a lot of full index scans (for example, SELECT col1 FROM foo, assuming that col1 is indexed).

Handler_read_key

The number of requests to read a row based on a key. If this value is high, it is a good indication that your tables are properly indexed for your queries.

Handler_read_last

The number of requests to read the last key in an index. With ORDER BY, the server will issue a first-key request followed by several next-key requests, whereas with ORDER BY DESC, the server will issue a last-key request followed by several previous-key requests.

Handler_read_next

The number of requests to read the next row in key order. This value is incremented if you are querying an index column with a range constraint or if you are doing an index scan.

Handler_read_prev

The number of requests to read the previous row in key order. This read method is mainly used to optimize ORDER BY ... DESC.

Handler_read_rnd

The number of requests to read a row based on a fixed position. This value is high if you are doing a lot of queries that require sorting of the result. You probably have a lot of queries that require MySQL to scan entire tables or you have joins that do not use keys properly.

Handler_read_rnd_next

The number of requests to read the next row in the data file. This value is high if you are doing a lot of table scans. Generally this suggests that your tables are not properly indexed or that your queries are not written to take advantage of the indexes you have.

Handler_rollback

The number of requests for a storage engine to perform a rollback operation.

Handler_savepoint

The number of requests for a storage engine to place a savepoint.

Handler_savepoint_rollback

The number of requests for a storage engine to roll back to a savepoint.

Handler_update

The number of requests to update a row in a table.

Handler_write

The number of requests to insert a row in a table.

Innodb_available_undo_logs

Innodb_available_undo_logs was removed in MySQL 8.0.2. The number of available rollback segments per tablespace may be retrieved using SHOW VARIABLES LIKE 'innodb_rollback_segments';

Innodb_buffer_pool_dump_status

The progress of an operation to record the pages held in the InnoDB buffer pool, triggered by the setting of innodb_buffer_pool_dump_at_shutdown or innodb_buffer_pool_dump_now.

For related information and examples, see Section 15.8.3.7, “Saving and Restoring the Buffer Pool State”.

Innodb_buffer_pool_load_status

The progress of an operation to warm up the InnoDB buffer pool by reading in a set of pages corresponding to an earlier point in time, triggered by the setting of innodb_buffer_pool_load_at_startup or innodb_buffer_pool_load_now. If the operation introduces too much overhead, you can cancel it by setting innodb_buffer_pool_load_abort.

For related information and examples, see Section 15.8.3.7, “Saving and Restoring the Buffer Pool State”.

Innodb_buffer_pool_bytes_data

The total number of bytes in the InnoDB buffer pool containing data. The number includes both dirty and clean pages. For more accurate memory usage calculations than with Innodb_buffer_pool_pages_data, when compressed tables cause the buffer pool to hold pages of different sizes.

Innodb_buffer_pool_pages_data

The number of pages in the InnoDB buffer pool containing data. The number includes both dirty and clean pages. When using compressed tables, the reported Innodb_buffer_pool_pages_data value may be larger than Innodb_buffer_pool_pages_total (Bug #59550).

Innodb_buffer_pool_bytes_dirty

The total current number of bytes held in dirty pages in the InnoDB buffer pool. For more accurate memory usage calculations than with Innodb_buffer_pool_pages_dirty, when compressed tables cause the buffer pool to hold pages of different sizes.

Innodb_buffer_pool_pages_dirty

The current number of dirty pages in the InnoDB buffer pool.

Innodb_buffer_pool_pages_flushed

The number of requests to flush pages from the InnoDB buffer pool.

Innodb_buffer_pool_pages_free

The number of free pages in the InnoDB buffer pool.

Innodb_buffer_pool_pages_latched

The number of latched pages in the InnoDB buffer pool. These are pages currently being read or written, or that cannot be flushed or removed for some other reason. Calculation of this variable is expensive, so it is available only when the UNIV_DEBUG system is defined at server build time.

Innodb_buffer_pool_pages_misc

The number of pages in the InnoDB buffer pool that are busy because they have been allocated for administrative overhead, such as row locks or the adaptive hash index. This value can also be calculated as Innodb_buffer_pool_pages_total − Innodb_buffer_pool_pages_free − Innodb_buffer_pool_pages_data. When using compressed tables, Innodb_buffer_pool_pages_misc may report an out-of-bounds value (Bug #59550).

Innodb_buffer_pool_pages_total

The total size of the InnoDB buffer pool, in pages. When using compressed tables, the reported Innodb_buffer_pool_pages_data value may be larger than Innodb_buffer_pool_pages_total (Bug #59550)

Innodb_buffer_pool_read_ahead

The number of pages read into the InnoDB buffer pool by the read-ahead background thread.

Innodb_buffer_pool_read_ahead_evicted

The number of pages read into the InnoDB buffer pool by the read-ahead background thread that were subsequently evicted without having been accessed by queries.

Innodb_buffer_pool_read_ahead_rnd

The number of “random” read-aheads initiated by InnoDB. This happens when a query scans a large portion of a table but in random order.

Innodb_buffer_pool_read_requests

The number of logical read requests.

Innodb_buffer_pool_reads

The number of logical reads that InnoDB could not satisfy from the buffer pool, and had to read directly from disk.

Innodb_buffer_pool_resize_status

The status of an operation to resize the InnoDB buffer pool dynamically, triggered by setting the innodb_buffer_pool_size parameter dynamically. The innodb_buffer_pool_size parameter is dynamic, which allows you to resize the buffer pool without restarting the server. See Configuring InnoDB Buffer Pool Size Online for related information.

Innodb_buffer_pool_wait_free

Normally, writes to the InnoDB buffer pool happen in the background. When InnoDB needs to read or create a page and no clean pages are available, InnoDB flushes some dirty pages first and waits for that operation to finish. This counter counts instances of these waits. If innodb_buffer_pool_size has been set properly, this value should be small.

Innodb_buffer_pool_write_requests

The number of writes done to the InnoDB buffer pool.

Innodb_data_fsyncs

The number of fsync() operations so far. The frequency of fsync() calls is influenced by the setting of the innodb_flush_method configuration option.

Innodb_data_pending_fsyncs

The current number of pending fsync() operations. The frequency of fsync() calls is influenced by the setting of the innodb_flush_method configuration option.

Innodb_data_pending_reads

The current number of pending reads.

Innodb_data_pending_writes

The current number of pending writes.

Innodb_data_read

The amount of data read since the server was started (in bytes).

Innodb_data_reads

The total number of data reads (OS file reads).

Innodb_data_writes

The total number of data writes.

Innodb_data_written

The amount of data written so far, in bytes.

Innodb_dblwr_pages_written

The number of pages that have been written to the doublewrite buffer. See Section 15.11.1, “InnoDB Disk I/O”.

Innodb_dblwr_writes

The number of doublewrite operations that have been performed. See Section 15.11.1, “InnoDB Disk I/O”.

Innodb_have_atomic_builtins

Indicates whether the server was built with atomic instructions.

Innodb_log_waits

The number of times that the log buffer was too small and a wait was required for it to be flushed before continuing.

Innodb_log_write_requests

The number of write requests for the InnoDB redo log.

Innodb_log_writes

The number of physical writes to the InnoDB redo log file.

Innodb_num_open_files

The number of files InnoDB currently holds open.

Innodb_os_log_fsyncs

The number of fsync() writes done to the InnoDB redo log files.

Innodb_os_log_pending_fsyncs

The number of pending fsync() operations for the InnoDB redo log files.

Innodb_os_log_pending_writes

The number of pending writes to the InnoDB redo log files.

Innodb_os_log_written

The number of bytes written to the InnoDB redo log files.

Innodb_page_size

InnoDB page size (default 16KB). Many values are counted in pages; the page size enables them to be easily converted to bytes.

Innodb_pages_created

The number of pages created by operations on InnoDB tables.

Innodb_pages_read

The number of pages read from the InnoDB buffer pool by operations on InnoDB tables.

Innodb_pages_written

The number of pages written by operations on InnoDB tables.

Innodb_row_lock_current_waits

The number of row locks currently being waited for by operations on InnoDB tables.

Innodb_row_lock_time

The total time spent in acquiring row locks for InnoDB tables, in milliseconds.

Innodb_row_lock_time_avg

The average time to acquire a row lock for InnoDB tables, in milliseconds.

Innodb_row_lock_time_max

The maximum time to acquire a row lock for InnoDB tables, in milliseconds.

Innodb_row_lock_waits

The number of times operations on InnoDB tables had to wait for a row lock.

Innodb_rows_deleted

The number of rows deleted from InnoDB tables.

Innodb_rows_inserted

The number of rows inserted into InnoDB tables.

Innodb_rows_read

The number of rows read from InnoDB tables.

Innodb_rows_updated

The number of rows updated in InnoDB tables.

Innodb_truncated_status_writes

The number of times output from the SHOW ENGINE INNODB STATUS statement has been truncated.

Key_blocks_not_flushed

The number of key blocks in the MyISAM key cache that have changed but have not yet been flushed to disk.

Key_blocks_unused

The number of unused blocks in the MyISAM key cache. You can use this value to determine how much of the key cache is in use; see the discussion of key_buffer_size in Section 5.1.8, “Server System Variables”.

Key_blocks_used

The number of used blocks in the MyISAM key cache. This value is a high-water mark that indicates the maximum number of blocks that have ever been in use at one time.

Key_read_requests

The number of requests to read a key block from the MyISAM key cache.

Key_reads

The number of physical reads of a key block from disk into the MyISAM key cache. If Key_reads is large, then your key_buffer_size value is probably too small. The cache miss rate can be calculated as Key_reads/Key_read_requests.

Key_write_requests

The number of requests to write a key block to the MyISAM key cache.

Key_writes

The number of physical writes of a key block from the MyISAM key cache to disk.

Last_query_cost

The total cost of the last compiled query as computed by the query optimizer. This is useful for comparing the cost of different query plans for the same query. The default value of 0 means that no query has been compiled yet. The default value is 0. Last_query_cost has session scope.

In MySQL 8.0.16 and later, this variable shows the cost of queries that have multiple query blocks, summing the cost estimates of each query block, estimating how many times non-cacheable subqueries are executed, and multiplying the cost of those query blocks by the number of subquery executions. (Bug #92766, Bug #28786951) Prior to MySQL 8.0.16, Last_query_cost was computed accurately only for simple, “flat” queries, but not for complex queries such as those containing subqueries or UNION. (For the latter, the value was set to 0.)

Last_query_partial_plans

The number of iterations the query optimizer made in execution plan construction for the previous query. Last_query_cost has session scope.

Locked_connects

The number of attempts to connect to locked user accounts. For information about account locking and unlocking, see Section 6.2.19, “Account Locking”.

Max_execution_time_exceeded

The number of SELECT statements for which the execution timeout was exceeded.

Max_execution_time_set

The number of SELECT statements for which a nonzero execution timeout was set. This includes statements that include a nonzero MAX_EXECUTION_TIME optimizer hint, and statements that include no such hint but execute while the timeout indicated by the max_execution_time system variable is nonzero.

Max_execution_time_set_failed

The number of SELECT statements for which the attempt to set an execution timeout failed.

Max_used_connections

The maximum number of connections that have been in use simultaneously since the server started.

Max_used_connections_time

The time at which Max_used_connections reached its current value.

Not_flushed_delayed_rows

This status variable is deprecated (because DELAYED inserts are not supported), and will be removed in a future release.

mecab_charset

The character set currently used by the MeCab full-text parser plugin. For related information, see Section 12.9.9, “MeCab Full-Text Parser Plugin”.

Ongoing_anonymous_transaction_count

Shows the number of ongoing transactions which have been marked as anonymous. This can be used to ensure that no further transactions are waiting to be processed.

Ongoing_anonymous_gtid_violating_transaction_count

This status variable is only available in debug builds. Shows the number of ongoing transactions which use gtid_next=ANONYMOUS and that violate GTID consistency.

Ongoing_automatic_gtid_violating_transaction_count

This status variable is only available in debug builds. Shows the number of ongoing transactions which use gtid_next=AUTOMATIC and that violate GTID consistency.

Open_files

The number of files that are open. This count includes regular files opened by the server. It does not include other types of files such as sockets or pipes. Also, the count does not include files that storage engines open using their own internal functions rather than asking the server level to do so.

Open_streams

The number of streams that are open (used mainly for logging).

Open_table_definitions

The number of cached table definitions.

Open_tables

The number of tables that are open.

Opened_files

The number of files that have been opened with my_open() (a mysys library function). Parts of the server that open files without using this function do not increment the count.

Opened_table_definitions

The number of table definitions that have been cached.

Opened_tables

The number of tables that have been opened. If Opened_tables is big, your table_open_cache value is probably too small.

Performance_schema_xxx

Performance Schema status variables are listed in Section 26.16, “Performance Schema Status Variables”. These variables provide information about instrumentation that could not be loaded or created due to memory constraints.

Prepared_stmt_count

The current number of prepared statements. (The maximum number of statements is given by the max_prepared_stmt_count system variable.)

Qcache_free_blocks

This status variable was removed in MySQL 8.0.3.

Qcache_free_memory

This status variable was removed in MySQL 8.0.3.

Qcache_hits

This status variable was removed in MySQL 8.0.3.

Qcache_inserts

This status variable was removed in MySQL 8.0.3.

Qcache_lowmem_prunes

This status variable was removed in MySQL 8.0.3.

Qcache_not_cached

This status variable was removed in MySQL 8.0.3.

Qcache_queries_in_cache

This status variable was removed in MySQL 8.0.3.

Qcache_total_blocks

This status variable was removed in MySQL 8.0.3.

Queries

The number of statements executed by the server. This variable includes statements executed within stored programs, unlike the Questions variable. It does not count COM_PING or COM_STATISTICS commands.

The discussion at the beginning of this section indicates how to relate this statement-counting status variable to other such variables.

Questions

The number of statements executed by the server. This includes only statements sent to the server by clients and not statements executed within stored programs, unlike the Queries variable. This variable does not count COM_PING, COM_STATISTICS, COM_STMT_PREPARE, COM_STMT_CLOSE, or COM_STMT_RESET commands.

The discussion at the beginning of this section indicates how to relate this statement-counting status variable to other such variables.

Rpl_semi_sync_master_clients

The number of semisynchronous slaves.

This variable is available only if the master-side semisynchronous replication plugin is installed.

Rpl_semi_sync_master_net_avg_wait_time

The average time in microseconds the master waited for a slave reply. This variable is always 0, is deprecated and it will be removed in a future version.

This variable is available only if the master-side semisynchronous replication plugin is installed.

Rpl_semi_sync_master_net_wait_time

The total time in microseconds the master waited for slave replies. This variable is always 0, is deprecated and it will be removed in a future version.

This variable is available only if the master-side semisynchronous replication plugin is installed.

Rpl_semi_sync_master_net_waits

The total number of times the master waited for slave replies.

This variable is available only if the master-side semisynchronous replication plugin is installed.

Rpl_semi_sync_master_no_times

The number of times the master turned off semisynchronous replication.

This variable is available only if the master-side semisynchronous replication plugin is installed.

Rpl_semi_sync_master_no_tx

The number of commits that were not acknowledged successfully by a slave.

This variable is available only if the master-side semisynchronous replication plugin is installed.

Rpl_semi_sync_master_status

Whether semisynchronous replication currently is operational on the master. The value is ON if the plugin has been enabled and a commit acknowledgment has occurred. It is OFF if the plugin is not enabled or the master has fallen back to asynchronous replication due to commit acknowledgment timeout.

This variable is available only if the master-side semisynchronous replication plugin is installed.

Rpl_semi_sync_master_timefunc_failures

The number of times the master failed when calling time functions such as gettimeofday().

This variable is available only if the master-side semisynchronous replication plugin is installed.

Rpl_semi_sync_master_tx_avg_wait_time

The average time in microseconds the master waited for each transaction.

This variable is available only if the master-side semisynchronous replication plugin is installed.

Rpl_semi_sync_master_tx_wait_time

The total time in microseconds the master waited for transactions.

This variable is available only if the master-side semisynchronous replication plugin is installed.

Rpl_semi_sync_master_tx_waits

The total number of times the master waited for transactions.

This variable is available only if the master-side semisynchronous replication plugin is installed.

Rpl_semi_sync_master_wait_pos_backtraverse

The total number of times the master waited for an event with binary coordinates lower than events waited for previously. This can occur when the order in which transactions start waiting for a reply is different from the order in which their binary log events are written.

This variable is available only if the master-side semisynchronous replication plugin is installed.

Rpl_semi_sync_master_wait_sessions

The number of sessions currently waiting for slave replies.

This variable is available only if the master-side semisynchronous replication plugin is installed.

Rpl_semi_sync_master_yes_tx

The number of commits that were acknowledged successfully by a slave.

This variable is available only if the master-side semisynchronous replication plugin is installed.

Rpl_semi_sync_slave_status

Whether semisynchronous replication currently is operational on the slave. This is ON if the plugin has been enabled and the slave I/O thread is running, OFF otherwise.

This variable is available only if the slave-side semisynchronous replication plugin is installed.

Rsa_public_key

This variable is available if MySQL was compiled using OpenSSL (see Section 6.3.3, “SSL Library-Dependent Capabilities”). Its value is the public key used by the sha256_password authentication plugin for RSA key pair-based password exchange. The value is nonempty only if the server successfully initializes the private and public keys in the files named by the sha256_password_private_key_path and sha256_password_public_key_path system variables. The value of Rsa_public_key comes from the latter file.

For information about sha256_password, see Section 6.4.1.2, “SHA-256 Pluggable Authentication”.

Secondary_engine_execution_count

For future use. This variable was added in MySQL 8.0.13.

Select_full_join

The number of joins that perform table scans because they do not use indexes. If this value is not 0, you should carefully check the indexes of your tables.

Select_full_range_join

The number of joins that used a range search on a reference table.

Select_range

The number of joins that used ranges on the first table. This is normally not a critical issue even if the value is quite large.

Select_range_check

The number of joins without keys that check for key usage after each row. If this is not 0, you should carefully check the indexes of your tables.

Select_scan

The number of joins that did a full scan of the first table.

Slave_heartbeat_period

This variable is obsolete and was removed in MySQL 8.0.1. Instead, use the HEARTBEAT_INTERVAL column of the replication_connection_configuration table.

Slave_last_heartbeat

This variable is obsolete and was removed in MySQL 8.0.1. Instead, use the LAST_HEARTBEAT_TIMESTAMP column of the replication_connection_status table.

Slave_open_temp_tables

The number of temporary tables that the slave SQL thread currently has open. If the value is greater than zero, it is not safe to shut down the slave; see Section 17.4.1.30, “Replication and Temporary Tables”. This variable reports the total count of open temporary tables for all replication channels.

Slave_received_heartbeats

This variable is obsolete and was removed in MySQL 8.0.1. Instead, use the COUNT_RECEIVED_HEARTBEATS column of the replication_connection_status table.

Slave_retried_transactions

This variable is obsolete and was removed in MySQL 8.0.1. Instead, use the COUNT_TRANSACTIONS_RETRIES column of the replication_applier_status table.

Slave_rows_last_search_algorithm_used

The search algorithm that was most recently used by this slave to locate rows for row-based replication. The result shows whether the slave used indexes, a table scan, or hashing as the search algorithm for the last transaction executed on any channel.

The method used depends on the setting for the slave_rows_search_algorithms system variable, and the keys that are available on the relevant table.

This variable is available only for debug builds of MySQL.

Slave_running

This variable is obsolete and was removed in MySQL 8.0.1. Instead, use the SERVICE_STATE column of the replication_connection_status and replication_applier_status tables.

Slow_launch_threads

The number of threads that have taken more than slow_launch_time seconds to create.

Slow_queries

The number of queries that have taken more than long_query_time seconds. This counter increments regardless of whether the slow query log is enabled. For information about that log, see Section 5.4.5, “The Slow Query Log”.

Sort_merge_passes

The number of merge passes that the sort algorithm has had to do. If this value is large, you should consider increasing the value of the sort_buffer_size system variable.

Sort_range

The number of sorts that were done using ranges.

Sort_rows

The number of sorted rows.

Sort_scan

The number of sorts that were done by scanning the table.

Ssl_accept_renegotiates

The number of negotiates needed to establish the connection.

Ssl_accepts

The number of accepted SSL connections.

Ssl_callback_cache_hits

The number of callback cache hits.

Ssl_cipher

The current encryption cipher (empty for unencrypted connections).

Ssl_cipher_list

The list of possible SSL ciphers (empty for non-SSL connections). If MySQL supports TLSv1.3, the value includes the possible TLSv1.3 ciphersuites. See Section 6.3.5, “Encrypted Connection Protocols and Ciphers”.

Ssl_client_connects

The number of SSL connection attempts to an SSL-enabled master.

Ssl_connect_renegotiates

The number of negotiates needed to establish the connection to an SSL-enabled master.

Ssl_ctx_verify_depth

The SSL context verification depth (how many certificates in the chain are tested).

Ssl_ctx_verify_mode

The SSL context verification mode.

Ssl_default_timeout

The default SSL timeout.

Ssl_finished_accepts

The number of successful SSL connections to the server.

Ssl_finished_connects

The number of successful slave connections to an SSL-enabled master.

Ssl_server_not_after

The last date for which the SSL certificate is valid. To check SSL certificate expiration information, use this statement:

mysql> SHOW STATUS LIKE 'Ssl_server_not%';
+-----------------------+--------------------------+
| Variable_name         | Value                    |
+-----------------------+--------------------------+
| Ssl_server_not_after  | Apr 28 14:16:39 2025 GMT |
| Ssl_server_not_before | May  1 14:16:39 2015 GMT |
+-----------------------+--------------------------+
Ssl_server_not_before

The first date for which the SSL certificate is valid.

Ssl_session_cache_hits

The number of SSL session cache hits.

Ssl_session_cache_misses

The number of SSL session cache misses.

Ssl_session_cache_mode

The SSL session cache mode.

Ssl_session_cache_overflows

The number of SSL session cache overflows.

Ssl_session_cache_size

The SSL session cache size.

Ssl_session_cache_timeouts

The number of SSL session cache timeouts.

Ssl_sessions_reused

How many SSL connections were reused from the cache.

Ssl_used_session_cache_entries

How many SSL session cache entries were used.

Ssl_verify_depth

The verification depth for replication SSL connections.

Ssl_verify_mode

The verification mode used by the server for a connection that uses SSL. The value is a bitmask; bits are defined in the openssl/ssl.h header file:
```
# define SSL_VERIFY_NONE                 0x00
# define SSL_VERIFY_PEER                 0x01
# define SSL_VERIFY_FAIL_IF_NO_PEER_CERT 0x02
# define SSL_VERIFY_CLIENT_ONCE          0x04
```

SSL_VERIFY_PEER indicates that the server asks for a client certificate. If the client supplies one, the server performs verification and proceeds only if verification is successful. SSL_VERIFY_CLIENT_ONCE indicates that a request for the client certificate will be done only in the initial handshake.

Ssl_version

The SSL protocol version of the connection (for example, TLSv1). If the connection is not encrypted, the value is empty.

Table_locks_immediate

The number of times that a request for a table lock could be granted immediately.

Table_locks_waited

The number of times that a request for a table lock could not be granted immediately and a wait was needed. If this is high and you have performance problems, you should first optimize your queries, and then either split your table or tables or use replication.

Table_open_cache_hits

The number of hits for open tables cache lookups.

Table_open_cache_misses

The number of misses for open tables cache lookups.

Table_open_cache_overflows

The number of overflows for the open tables cache. This is the number of times, after a table is opened or closed, a cache instance has an unused entry and the size of the instance is larger than table_open_cache / table_open_cache_instances.

Tc_log_max_pages_used

For the memory-mapped implementation of the log that is used by mysqld when it acts as the transaction coordinator for recovery of internal XA transactions, this variable indicates the largest number of pages used for the log since the server started. If the product of Tc_log_max_pages_used and Tc_log_page_size is always significantly less than the log size, the size is larger than necessary and can be reduced. (The size is set by the --log-tc-size option. This variable is unused: It is unneeded for binary log-based recovery, and the memory-mapped recovery log method is not used unless the number of storage engines that are capable of two-phase commit and that support XA transactions is greater than one. (InnoDB is the only applicable engine.)

Tc_log_page_size

The page size used for the memory-mapped implementation of the XA recovery log. The default value is determined using getpagesize(). This variable is unused for the same reasons as described for Tc_log_max_pages_used.

Tc_log_page_waits

For the memory-mapped implementation of the recovery log, this variable increments each time the server was not able to commit a transaction and had to wait for a free page in the log. If this value is large, you might want to increase the log size (with the --log-tc-size option). For binary log-based recovery, this variable increments each time the binary log cannot be closed because there are two-phase commits in progress. (The close operation waits until all such transactions are finished.)

Threads_cached

The number of threads in the thread cache.

Threads_connected

The number of currently open connections.

Threads_created

The number of threads created to handle connections. If Threads_created is big, you may want to increase the thread_cache_size value. The cache miss rate can be calculated as Threads_created/Connections.

Threads_running

The number of threads that are not sleeping.

Uptime

The number of seconds that the server has been up.

Uptime_since_flush_status

The number of seconds since the most recent FLUSH STATUS statement.
