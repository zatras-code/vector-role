# Ansible Role: Vector

Роль Ansible для установки и настройки **Vector** — агента сбора и обработки логов.

Роль предназначена для использования в составе playbook и обеспечивает идемпотентную установку Vector как systemd-сервиса.

---

## Возможности роли

- Загрузка и установка Vector из официального дистрибутива
- Создание необходимых директорий
- Деплой конфигурации через Jinja2-шаблон
- Настройка `data_dir`
- Создание systemd unit-файла
- Запуск и включение сервиса Vector
- Корректная работа в `--check` режиме
- Идемпотентность при повторных запусках

---

## Требования

- Ansible >= 2.14
- ОС: Debian / Ubuntu
- Доступ по SSH
- Права `sudo` (become задаётся на уровне play)

---

## Переменные роли

Все переменные задаются в `defaults/main.yml` и могут быть переопределены пользователем.

| Переменная | Описание | Значение по умолчанию |
|----------|----------|------------------------|
| `vector_version` | Версия Vector | `0.34.1` |
| `vector_install_dir` | Каталог распаковки | `/opt/vector` |
| `vector_config_dir` | Каталог конфигурации | `/etc/vector` |
| `vector_config_file` | Имя конфигурационного файла | `vector.yaml` |
| `vector_data_dir` | Каталог данных | `/var/lib/vector` |
| `vector_bin_path` | Путь к бинарнику | `/usr/local/bin/vector` |
| `vector_archive_url` | URL дистрибутива | рассчитывается автоматически |

---

## Шаблоны

- `templates/vector.yaml.j2` — основной конфигурационный файл Vector

---

## Handlers

- `Reload systemd` — перезагрузка systemd
- `Restart vector` — перезапуск сервиса Vector

---

## Пример использования роли

```yaml
- name: Install Vector
  hosts: vector
  become: true
  roles:
    - vector_role
```

---