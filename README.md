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
### [reset]()
* Удаление stack servers.
* Docker prune.
* Удаление docker сетей.
* Удаление docker volumes.
* Расформирование swarm кластера.
* Перезапуск docker.
### [init]()
* Создание мастера и join ссылок.
* Создание подсети.
* Загрузка утилиты etcdctl.
* Создание сертификатов etcd и загрузка в ansible.
* Выгрузка [load-balancer.conf]()
### [join]()
* Подключение NODE к кластеру swarm.
* Выгрузка сертификатов etcd.
* Выгрузка [load-balancer.conf]()
### [deploy]()
* Выгрузка [compose.yaml]()
* Создание ссылки на [discovery](https://discovery.etcd.io/).
* Развёртывание.































