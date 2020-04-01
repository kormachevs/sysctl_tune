# sysctl_tune


Использование:

    git clone https://github.com/kormachevs/sysctl_tune.git

    cd ./sysctl_tune

#### Поправить hosts, заполнить своими данными

    ansible-playbook sysctl_tune.yaml

##### Плейбук кастомизирует параметры ядра, применяет их на лету и записывает в файл /etc/sysctl.conf для восстановления значений после перезагрузки OS.

        net.ipv4.ip_forward=1
        net.ipv4.ip_nonlocal_bind=1
        vm.swappiness=5
        fs.file-max=65536
        vm.vfs_cache_pressure=1000
        net.ipv6.conf.all.disable_ipv6=1
        vm.overcommit_memory=2
        vm.overcommit_ratio=50
        
Тестирование роли на OS: Ubuntu 16.04, Ubuntu 18.04


Роль не стал оформлять т.к плейбук состоит из 1 таска... 
___
PS: 

Overcommit - стратегия выделения памяти, когда операционная система разрешает приложениям занимать больше виртуальной памяти, чем доступно в системе. 

Существует 3 стратегии: 

 0 (по умолчанию) — ядро использует эвристический алгоритм для расчета перерасхода памяти, принимая во внимание объем доступной памяти и число неверных запросов. Но поскольку выделение памяти осуществляется на основе эвристического, а не точного алгоритма, это может привести к превышению допустимой нагрузки на память.

1 — ядро не обрабатывает перерасход памяти. При этом вероятность превышения нагрузки на память возрастает, но в то же время увеличивается производительность задач, активно использующих память.

2 — отказ обработки запросов, запрашивающих память, размер которой превышает суммарный размер памяти пространства подкачки и ОЗУ в соответствии с overcommit_ratio. Если overcommit_ratio < 100, система всегда будет выделять память только если она подкреплена реальными страницами в ОЗУ или свопе

      Commit_Limit = total_swap + total_ram * overcommit_ratio / 100

Info from RedHat: This setting is only recommended for systems with swap areas larger than physical memory.

https://access.redhat.com/documentation/ru-ru/red_hat_enterprise_linux/6/html/performance_tuning_guide/s-memory-captun

