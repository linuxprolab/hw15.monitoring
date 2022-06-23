# Домашнее задание 15. Настройка мониторинга.
Настроить дашборд с 4-мя графиками:
- память
- процессор
- диск
- сеть
Мониторить будем с помощью Prometheus+Grafana.
## Состав стенда.
Развернем следующие виртуалки
- `system` - хост, с которого будем получать метрики
- `monitorint` - хост с развернутыми Prometheus+Grafana в докер-контейнерах

## Запуск и проверка
- Клонируем репозиторий:
```
git clone https://github.com/linuxprolab/hw15.monitoring
cd hw15.monitoring
```
- Поднимаем VM:
```
vagrant up
```
- Запускаем плейбук ansible:
```
ansible-playbook playbooks/main.yml -i inventories/all.yml 
```
- Web GUI Prometheus должна быть доступна по  URL `http://127.0.0.1:9090/`.
- Dashboard Grafana должна быть доступна по  URL `http://127.0.0.1:3000/`.