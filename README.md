# swarm
## Описание
* Установка swarm.
* Установка кластера etcd.
  * Кластер размером по количеству control серверов (3).
  * Масштабируется при помощи [discovery](https://discovery.etcd.io/).
  * База хранится на NODE, бекап делается раз в час (медленный NAS).
  * Доступ по клиентским сертификатам.
* Установка балансировщика nginx

## Dependency
| Дополнительно | Значение                                              | Comment |
|:--------------|:------------------------------------------------------|:--------|
| Образ         | [ansible](https://github.com/FZEN475/ansible-image)   |         |
| Библиотеки    | [Library](https://github.com/FZEN475/ansible-library) |         |

## Этапы
### [reset](https://github.com/FZEN475/swarm/blob/main/playbooks/_1_swarm/_0_reset.yaml)
* Удаление stack servers.
* Docker prune.
* Удаление docker сетей.
* Удаление docker volumes.
* Расформирование swarm кластера.
* Перезапуск docker.
### [init](https://github.com/FZEN475/swarm/blob/main/playbooks/_1_swarm/_1_init.yaml)
* Создание мастера и join ссылок.
* Создание подсети.
* Загрузка утилиты etcdctl.
* Создание сертификатов etcd и загрузка в ansible.
* Выгрузка [load-balancer.conf](https://github.com/FZEN475/swarm/blob/main/config/load-balancer.conf)
### [join](https://github.com/FZEN475/swarm/blob/main/playbooks/_1_swarm/_2_join.yaml)
* Подключение NODE к кластеру swarm.
* Выгрузка сертификатов etcd.
* Выгрузка [load-balancer.conf](https://github.com/FZEN475/swarm/blob/main/config/load-balancer.conf)
### [deploy](https://github.com/FZEN475/swarm/blob/main/playbooks/_1_swarm/_3_deploy.yaml)
* Выгрузка [compose.yaml](https://github.com/FZEN475/swarm/blob/main/config/compose.yaml)
* Создание ссылки на [discovery](https://discovery.etcd.io/).
* Развёртывание.































