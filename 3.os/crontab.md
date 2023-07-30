## crontab 定时任务

- 问题：使用crontab处理定时任务，碰到并发问题咋办？

- 背景：linux 启动进程处理每个定时任务，如果任务运行时间比较耗时，但定时间隔较短，导致任务并发执行，可能产生任务堆积和消耗资源（如果设定了任务每分钟执行一次，但有可能一分钟内任务并没有执行完成，这时系统会再执行任务。导致两个相同的任务在执行。）

- 解决1：[linux flock文件加锁方式](https://blog.csdn.net/fdipzone/article/details/38284009?spm=1001.2101.3001.6650.4&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-4-38284009-blog-83344742.pc_relevant_3mothn_strategy_and_data_recovery&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-4-38284009-blog-83344742.pc_relevant_3mothn_strategy_and_data_recovery&utm_relevant_index=5)

- 解决2： 引入消息队列（比如分布式任务队列 celery定时任务）[链接](https://blog.51cto.com/u_15284125/2992991)