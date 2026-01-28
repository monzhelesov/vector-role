# Ansible Role: Vector

Ansible role для установки и настройки Vector - инструмента для сбора и обработки логов.

## Требования

- Ansible 2.9+
- Целевая ОС: Ubuntu/Debian
- Права sudo на целевом хосте

## Переменные роли

### Defaults (defaults/main.yml)

| Переменная | Значение по умолчанию | Описание |
|------------|----------------------|----------|
| `vector_version` | `0.34.0` | Версия Vector для установки |
| `vector_dir` | `/opt/vector` | Директория установки Vector |
| `vector_arch` | `x86_64-unknown-linux-gnu` | Архитектура системы |
| `vector_url` | `https://packages.timber.io/vector/...` | URL для скачивания архива |
| `vector_bin_path` | `{{ vector_dir }}/vector-{{ vector_arch }}/bin/vector` | Путь к бинарнику Vector |

### Vars

Дополнительные переменные можно определить в `vars/main.yml` или при вызове роли.

## Зависимости

Нет зависимостей от других ролей.

## Пример использования

```yaml
- hosts: vector
  become: true
  roles:
    - role: vector-role
      vars:
        vector_version: "0.34.0"
```

## Шаблоны

### vector.toml.j2

Конфигурационный файл Vector. По умолчанию необходимо создать в `templates/vector.toml.j2` в соответствии с вашими требованиями.

Пример минимальной конфигурации:
```toml
[sources.in]
type = "stdin"

[sinks.out]
type = "console"
inputs = ["in"]
encoding.codec = "json"
```

## Handlers

- `Restart vector` - перезапуск сервиса Vector

## Теги

Версионирование следует семантическому версионированию (SemVer):
- MAJOR.PATCH (1.0.0)

## Лицензия

MIT

## Автор

Roman