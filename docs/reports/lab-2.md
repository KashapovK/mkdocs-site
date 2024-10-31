# mkdocs-site

Автор: Константин Кашапов

## Отчёт - Практика 2

### 1. Обновление метаданных

Файл `mkdocs.yml`

```yml
site_name: MkDocs-site
site_description: Сайт на Python и MkDocs
site_author: Константин Кашапов
copyright: '2024'

repo_url: https://github.com/kashapovk/mkdocs-site
```

### 2. Создание директории и корневого файла темы

``` bash
mkdir custom-theme
cd custom-theme
```

```bash
touch main.html
```

### 3. Подключение темы

В файле `mkdocs.yml` добавяю тему через `theme`. Использую стандарную тему `name: mkdocs`. Директорию для темы через `custom_dir`.

`color_mode` цветовой темы установлен в `auto`. `user_color_mode_toggle` позволяет отобразить ручное управление темой для пользователя.

```yml
theme:
  name: mkdocs
  color_mode: auto
  user_color_mode_toggle: true
  custom_dir: 'custom-theme/'
```

### 4. Коневой файл темы

Наследование содержимого от стандартной темы через вставку при помощи шаблонизатора

```html
{% extends "base.html" %}
```

```html
{% block htmltitle %}
<title>{{ config.site_name }}</title>
{% endblock %}
```

### 5. Кастомизация

Стандартные кнопки для поиска и навигации убраны:

```html
{%- block search_button %}

{%- endblock %}

{%- block next_prev %}

{%- endblock %}
```

Использование кастомного footer

```html
{% block footer %}
<hr>
<p>
    {{config.site_author}}, {{config.copyright}}<br>
    {{config.site_description}}
</p>
<hr>
{% endblock %}
```

### 6. CSS

CSS файл располагаю в `css/overrides.css`.

Шаблон `{{ super() }}` наследует содержимое блока

```html
{% block styles %}
{{ super() }}
<link href="{{ 'css/overrides.css'|url }}" rel="stylesheet">
{% endblock %}
```

Добавляю стили

```css
:root {
    --bs-font-sans-serif: "Inter";
}

:root, [data-bs-theme="light"] {
    --bs-primary: #28d84e;
    --bs-primary-rgb: 186, 104, 200;

    --bs-link-color: #398e43;
    --bs-link-color-rgb: 149, 117, 205;

    --bs-link-hover-color: #1d6128;
    --bs-link-hover-color-rgb: 126, 87, 194;
}

[data-bs-theme="dark"] {

    --bs-primary: #22ca32;
    --bs-primary-rgb: 171, 71, 188;

    --bs-link-color: #087828;
    --bs-link-color-rgb: 149, 117, 205;

    --bs-link-hover-color: #07530e;
    --bs-link-hover-color-rgb: 126, 87, 194;
}

body::before {
    background: none;
}

.navbar.bg-primary {
    background-image: none;
}

.content-block {
    border: #42a529 6px;
}

footer {
    font-weight: 400;
}
```
