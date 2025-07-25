# Краткое описание

Проект создавался в рамках отбора на стажировку в Avito 2025. С ТЗ можно ознакомиться [тут](https://github.com/avito-tech/tech-internship/blob/main/Tech%20Internships/Frontend/Frontend-trainee-assignment-winter-2025/Frontend-trainee-assignment-winter-2025.md)

# Инструкция по развёртыванию с Docker

- **ВАЖНО!** Клиент и сервер в проекте являются git-подмодулями. Поэтому для клонирования репозитория с подмодулями выполните:
  ```
  git clone --recurse-submodules https://github.com/HuggySoul/advertisement-platform.git
  ```
- Запустите Docker или установите с [официального сайта](https://www.docker.com/products/docker-desktop/)
- Выполните команду для сборки проекта в корневой папке проекта

  ```sh
  docker compose build
  ```

- Затем выполните команду для запуска контейнеров в корневой папке проекта

  ```sh
  docker compose up
  ```

- Перейдите по адресу http://localhost:8080/list для просмотра клиентской части
- С конфигурацией сервера можно ознакомиться [на его странице](https://github.com/HuggySoul/ad-server/blob/master/README-API.md)

# Инструкция по развёртыванию с npm

### Запуск сервера

- **ВАЖНО!** Клиент и сервер в проекте являются git-подмодулями. Поэтому для клонирования репозитория с подмодулями выполните:

  ```
  git clone --recurse-submodules https://github.com/HuggySoul/advertisement-platform.git
  ```

- Перейдите в директорию `./ad-server` и выполните команду для установки node-модулей:
  ```sh
  npm i
  ```
- В этой же директории для запуска выполните:
  ```sh
  npm start
  ```

### Запуск клиента

- Перейдите в директорию `./ad-client` и выполните команду для установки node-модулей:
  ```sh
  npm i
  ```
- В этой же директории для запуска в режиме разработки:
  ```sh
  npm run dev
  ```
- Перейдите по адресу `http://localhost:8080/list`
- Более подробно с тем, какие команды для запуска доступны можно ознакомиться [в репозитории клиента](https://github.com/HuggySoul/ad-client)

# Клиент

Структура построена по принципу FSD, но с некоторыми упрощениями из-за небольшого размера проекта:

- всего в проекте 3 слоя - app, pages, shared
- Разрешены кросс-импорты между слайсами в shared

FSD выбрал по причине того, что с ним имею больший опыт взаимодействия, по сравнению с другими подходами.

### Используемые технологии и обоснование

- Vite для сборки проекта. Очень прост в настройке, что актуально в условиях ограниченного времени.
- Redux. Выбрал так как имею больший опыт использования, по сравнению с другими стейт-менеджерами. В ходе разработки сложилось так, что глобальные стейты для передачи данных между слайсами или сегментами не потребовались. Все данные передаются локально без пропс-дриллинга, с использованием стандартных хуков (присутствует проекте из-за RTK Query).
- RTK Query для работы с API. Использовал впервые, так как планировал его применять в связке с Redux. Первое впечатление: предоставляет довольно удобное api в виде хуков для взаимодействия с сервером. Из минусов - чрезмерное удобство использования api провоцирует хранить меньше стейтов на клиенте и чаще запрашивать данные :)
- React Hook form для работы с формами. Очень удобная библиотека, позволяющая уменьшить количество кода, который необходим для валидации и построения форм.
- esLint. Идёт вместе с Vite, часто помогает избегать ошибок при написании кода.
- prettier(в проекте нет, использовал как расширение). Давно его использую для форматирования кода, удобен, относительно гибок в настройке.

### Замечания по реализации функциональных требований

Так как изначально пошёл по пути серверной пагинации и отказа от хранения сразу всех объявлений на клиенте, то это повлекло необходимость модификации серверного API для реализации большинства фич.

# Сервер

Был добавлен метод поиска, а также добавлена обработка query-параметров для некоторых запросов. Более подробно с api и конфигурацией сервера можно ознакомиться [в его репозитории](https://github.com/HuggySoul/ad-server/blob/master/README-API.md)
