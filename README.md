# sysctl_tune
Роль не стал оформлять т.к плейбук состоит из 1 таска... 

  https://access.redhat.com/documentation/ru-ru/red_hat_enterprise_linux/6/html/performance_tuning_guide/s-memory-captun
  This setting is only recommended for systems with swap areas larger than physical memory.
  Commit_Limit total_swap + total_ram * overcommit_ratio / 100
  ratio < 100, система всегда будет выделять память только если она подкреплена реальными страницами в ОЗУ или свопе

