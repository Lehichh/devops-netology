# devops-netology
**Sarkisyan Aleksey**

**Выполнение задания 3.4 ОС**

**1.**

https://yapx.ru/v/PQqqw

**2.**


**CPU**
node_cpu_seconds_total{cpu="0",mode="idle"} 165950.44

node_cpu_seconds_total{cpu="0",mode="steal"} 0

node_cpu_seconds_total{cpu="0",mode="system"} 11.33

node_cpu_seconds_total{cpu="0",mode="user"} 8.64


**Memory**

node_memory_Active_bytes 4.51411968e+08

node_memory_MemFree_bytes 8.915968e+08

node_memory_MemTotal_bytes 2.058694656e+09


**Disk**

node_disk_write_time_seconds_total{device="sda"} 40.548

node_disk_read_time_seconds_total{device="sda"} 4.331

**Network**

node_network_speed_bytes{device="eth0"} 1.25e+08

node_network_transmit_bytes_total{device="eth0"} 1.705015e+07

node_network_receive_bytes_total{device="eth0"} 6.3860349e+07


**3.**

https://yapx.ru/v/PRPeD

**4.**

Можно.

vagrant@vagrant:~$ dmesg |grep virt

0.001572] CPU MTRRs all blank - virtualized system.

0.060809] Booting paravirtualized kernel on KVM

0.199759] Performance Events: PMU not available due to virtualization, using software events only.

2.120526] systemd[1]: Detected virtualization oracle.


**5.**

**fs.nr_open** - это системное ограничение, раное **1048576**

**ulimit -n *число*** с ним как я понял можно задавать мягкие и жесткие параметры, но это только для текущего терминала. Для постоянных ограничений нужно настроивать параметр **nofile** в **/etc/security/limits.conf** и **/etc/security/limits.d/**

**6.**

https://yapx.ru/v/PRcDM

**7.**

Это **fork-bomb**(форма атаки), я так понимаю функция, которая вызывает саму себя плодя процессы, кстати ограничение процессов **nproc** в том же **/etc/security/limits.conf** из 5-то задания, поможет избежать этого. Можно так же на терминал задать число процессов **ulimit -u *число***.

в одном месте вычитал что тут можно задать количество **/proc/sys/kernel/pid_max**

а механизм наверное этот **cgroup: fork rejected by pids controller in /user.slice/user-1000**