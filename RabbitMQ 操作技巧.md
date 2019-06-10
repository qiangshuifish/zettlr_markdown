# RabbitMQ 操作技巧


1. 两个 RabbitMQ 服务必须相互 ping 得才行
2. ``rabbitmqctl stop`` 停止 RabbitMQ 服务和当前 erlang 节点（虚拟机）， ``rabbitmqctl stop_app`` 是停止 RabbitMQ 服务，有些操作是 erlang 节点存活是才能进行的，彻底杀死 RabbitMQ 需要停止整个 erlang 虚拟机。``rabbitmqctl shutdown`` 停止 RabbitMQ 服务和当前 erlang 节点（虚拟机），和``rabbitmqctl stop``不同的是，``rabbitmqctl stop``需要 pid （貌似都不要V3.7.15验证）
3. 当集群内有机器掉线时，重新连接后，可能出现集群内两台机器相互发现不了对方的情况。此时只要重启其中一台即可``rabbitmqctl stop_app``,``rabbitmqctl start_app``。