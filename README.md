# swarm
## Description
* Кластер etcd.
  * Кластер размером по количеству control серверов (3).
  * Поиск реплик [discovery](https://discovery.etcd.io/).
  * База хранится локально, бекап раз в час kubernetes cron-job (медленный NAS).
  * Доступ по клиентским сертификатам.
* Nginx балансировщик.

## Dependency
* [Образ](https://github.com/FZEN475/ansible-image)
* [Library](https://github.com/FZEN475/ansible-library)

<details><summary> .env </summary>

```properties
ANSIBLE_REPO="https://github.com/FZEN475/swarm.git"
#GIT_EXTRA_PARAM="-btemp_branch"
SECURE_SERVER=""
SECURE_PATH=""
LIBRARY="https://github.com/FZEN475/ansible-library.git"
```
</details>

## Stages
### [reset](https://github.com/FZEN475/swarm/blob/main/playbooks/_1_swarm/_0_reset.yaml)
* Удаление stack servers.
* Docker prune.
* Удаление docker сетей.
* Удаление docker volumes.
* Расформирование swarm кластера.
* Перезапуск docker.
### [init](https://github.com/FZEN475/swarm/blob/main/playbooks/_1_swarm/_1_init.yaml)
* Создание мастера и join ссылок (в контейнере).
* Создание подсети.
* Установка etcdctl.
* Создание сертификатов etcd и загрузка в контейнер.
* Подготовка директорий.
* Выгрузка [load-balancer.conf](https://github.com/FZEN475/swarm/blob/main/config/load-balancer.conf)
### [join](https://github.com/FZEN475/swarm/blob/main/playbooks/_1_swarm/_2_join.yaml)
* Подключение NODE к кластеру swarm.
* Подготовка директорий.
* Выгрузка сертификатов etcd.
* Выгрузка [load-balancer.conf](https://github.com/FZEN475/swarm/blob/main/config/load-balancer.conf)
### [deploy](https://github.com/FZEN475/swarm/blob/main/playbooks/_1_swarm/_3_deploy.yaml)
* Выгрузка [compose.yaml](https://github.com/FZEN475/swarm/blob/main/config/compose.yaml)
* Создание ссылки на [discovery](https://discovery.etcd.io/).
* Развёртывание.
