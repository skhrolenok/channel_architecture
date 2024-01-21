---
theme: default
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shikiji
lineNumbers: true
info: |
  ## Channel architecture
  Presentation slides

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
transition: slide-left
title: Канальная архитектура
mdc: true
---

# Канальная архитектура

<div>Организация, Проблемы, Решения</div>


<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
Комментарии к слайду:

Слайд приветствие, анонс темы митапа
-->

---
transition: fade-out
---

# Темы для обсуждения

- 📝 **Каналы** - классификация каналов сервисного обслуживания
- 🎯 **Проблемы** - проблемы канальной архитектуры
- 🧑‍💻 **Классическая канальная архитектура** - составные части архитектуры
- 🚧 **Инфраструктура** - связанные с канальной архитектурой инфраструктурные компоненты
- 🚦 **Пользовательский доступ** - доступ к сервису, предоставляемой услуге
- 🎥 **Пользовательская сессия** - управление пользовательской сессией
- 🚲 **Организация API** - принципы, рекомендации и паттерны
- 📤 **Backend For Frontend** - роль BFF в канальной архитектуре
- 🛠 **API Gateway** - когда необходимо использовать паттерн

<!--
Комментарии к слайду:
Перечисление тем для обсуждения +тезисно о чем будет идти речь
Каналы - что такое каналы в контексте архитектуры,какие каналы бывают
Проблемы - проблемы типа множественных запросов к различным сервисам в рамка одной задачи,агрегирования запросов, интеграции с сервисами и тд
Классическая канальная архитектура - что из себя представляет канальная архитектура с различных точек зрения, примеры с диаграммами
Инфраструктура - различные инфраструктурные сервисы (сервисы, как правило предоставляемые облачной инфрой) связанные с канальной архитектурой
Пользовательский доступ - Пользователи и клиенты, в контексте канальной архитектуры, доступ к сервисам
Пользовательская сессия - Управление сессией, компоненты для реализации
Организация API - принципы построения апи в контексте канальной архитектуры
Backend For Frontend - паттерн BFF как часть канальной архитектуры
API Gateway - роль api gateway-я в канальной архитектуре и почему от него крайне плохо отказываться
-->

---
layout: image-right
image: https://img.freepik.com/free-vector/scan-me-qr-code_78370-2915.jpg?w=1480&t=st=1705516257~exp=1705516857~hmac=136818dc9d9054ad1295d3ddf4295778e45c3e4eed619476f9831cc70abf0171
---

# Содержание

<Toc maxDepth="1"></Toc>

<!-- 
Комментарии к слайду:
Слайд с содержанием и qr-code ссылкой на презентацию
-->

---
transition: slide-up
level: 1
preload: false
---

# Каналы

<div>
«<u>Канал</u> обслуживания клиентов» — это способ предложить/предоставить и организовать обслуживание <u>клиента</u>
</div>

<br>

<div v-motion
    :initial="{ x: -80, opacity: 0}"
    :enter="{ x: 0, opacity: 1, transition: { delay: 2000, duration: 1000 } }">
«<u>Канальная архитектура</u>» - организация программной системы по обслуживанию <u>клиента</u>
</div>

<br>

## Типы каналов

|     |     |
| --- | --- |
| Самообслуживание | веб, мобильное приложение |
| Агенты | колл-центр, точки интереса |
| Партнеры | ATM, 3-rd party shops |

<!-- Определение канала, и чем является канальная архитектура - организацией программной системы, 
со всеми компонентами их свойствами, связями. Разделение каналов по типу участникам участвующим в обслуживании клиента
-->

---
transition: slide-left
layout: image-right
image: https://www.commbox.io/wp-content/uploads/2019/10/52-1-1024x600.jpg
level: 2
---

# Самообслуживание

<div>Клиент обслуживает себя сам самостоятельно - покупка товара через интернет-магазин</div>

```mermaid {scale: 0.8, alt: 'Self-service diagram'}
erDiagram
    Client ||--|{ Website : uses
    Website ||--|{ Service : request
    Client ||--|{ Mobile_app : uses
    Mobile_app ||--|{ Service : request
```

<!-- Тип канала - самообслуживание, вероятно самый популярный с которым приходилось иметь дело с точки зрения разработки:
мобильные приложения, веб-сайты и тд, всё где клиент обслуживает себя сам самостоятельно - например покупка товара через интернет-магазин
-->

---
transition: slide-left
layout: image-right
image: https://images.ctfassets.net/3viuren4us1n/9JeAYuib2oE0QQYawCaqg/c857c8899b9461528089c297b30ec06d/empowering-agents.jpg
level: 2
---

# Агенты

<div>Клиент делегирует запрос услуги <u>агенту</u></div>

```mermaid {scale: 0.65, alt: 'Agents diagram'}
erDiagram
    Client ||--|{ Agent : delegate_request
    Agent ||--|{ Call_center : uses
    Agent ||--|{ Point_of_service : uses
    Call_center ||--|{ Service : request
    Point_of_service ||--|{ Service : request
```

<!-- Клиент делегирует запрос услуги агенту, а тот её выполняет
используя соответствующий сервис
-->

---
transition: slide-left
layout: image-right
image: https://www.thoughtco.com/thmb/nW1rRXA8oe3PzL6WVLrz2NGTgh8=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/thailand-atm-money-56a378765f9b58b7d0d21946.jpg
level: 2
---

# Партнеры

<div>Клиент пользуется сервисом партнеров</div>

```mermaid {scale: 0.9, alt: 'Partners diagram'}
erDiagram
    Client ||--|{ ATM : uses
    Client ||--|{ Partners_shop : uses
    ATM ||--|{ Service : request
    Partners_shop ||--|{ Service : request
```

<!-- Клиент использует не целевой (конечный) сервис, а сервис партнёров, по какой-либо причине
партнерский сервис предоставляя услугу, использует в том числе и целевой сервис
 -->

---
transition: slide-up
level: 2
---

# Процесс предоставления услуги

<div>Процедуры и шаги для предоставления сервиса</div>

<br>

```mermaid {scale: 0.57, alt: 'Service delivery process diagram'}
journey
    title Service delivery process
    section Client
      Questsions, needs: 7: Client
      Desires, preferences: 6: Client
      to matching service: 5: Client, Service
    section Service provider
      website, email: 4: Client, Service
      texts, description: 3: Client, Service
      procedures, rules: 3: Client, Service
      service, case data: 3: Client, Service
```

<!-- Процесс предоставления услуги состоит из нескольких шагов
начинаем с потребностей (хотелок) и вопросов клиента, его предпочтений
и 'приходим' к соответствующему сервису. 
Далее по каналу предоставляем услугу, выполняем бизнес логику и тд
 -->

<!-- <img src="/service_delivery.png" class="h-full rounded shadow" /> -->

---
transition: slide-left
layout: image-right
image: https://img.freepik.com/premium-vector/sets-people-talking-speaking-each-other-collection-chatting-men-women-with-speech-bubbles-isolated-white-background-colorful-vector-illustration-flat-cartoon-style_7545-316.jpg?w=1800
level: 2
---

# Процесс предоставления услуги

<br>

## Участники процесса

|     |     |
| --- | --- |
| Клиенты | используют сервис |
| Сервисы | реализуют услугу |
| Каналы | способ предоставить услугу |

<!-- С точки зрения участников в процессе участвуют клиенты - им нужна услуга
сервисы - они услугу реализуют и каналы - они услугу предоставляют, точка входа в сервис
(еще есть сервис провайдер - это больше внутренности организации сервиса)
-->

---
transition: slide-left
layout: image-right
image: https://www.detrack.com/wp-content/uploads/2022/08/retail-delivery-service-scaled.jpg
level: 2
---

# Процесс предоставления услуги

<br>

## Процедура и активности

|     |     |
| --- | --- |
| Клиент | ищет и выбирает сервис через канал обслуживания |
| Сервис | доставка услуги через выбранный канал |
| Провайдер | выполняет все внутреннии процедуры для услуги |

<!-- С точки зрения активности, 
клиент выбирает сервис, сервис предоставляет услугу через канал
а провайдер выполняет внутренние процессы
-->

---
transition: slide-up
layout: image-right
image: https://media0.giphy.com/media/mq5y2jHRCAqMo/giphy.gif?cid=6c09b95236ohii9vhopbvrwgfp74eh1910yhigmmvrlszjx2&ep=v1_gifs_search&rid=giphy.gif&ct=g
---

# Проблемы

- 📝 **Уязвимость канала** - защищенность канала услуг от внешнего воздействия
- 🎯 **Работоспособность сервиса** - зависимость работы сервиса от канала услуг
- 🧑‍💻 **Приватность клиента** - предотвращение утечки персональных данных

<!-- В таком процессе неизбежны проблемы и сложности
связанные с уязвимостью канала так как он расчитан на внешнее воздействие
Работа самого сервиса с учетом различных уязвимостей и факторов
Приватность данных клиента при работе сервиса и предоставлению услуги
-->

---
transition: slide-left
level: 2
---

# Уязвимость канала

<br>

## Сценарий - денежный перевод

<br>

- 📝 **Клиент** - использует услугу перевода денег
- 🎯 **Сервис** - состоит из "fiat" системы, крипто кошелька, системы клиентского оповещения
- 🧑‍💻 **Процедура** - мобильное приложение пошагово использует сервисы для перевода денег

---
transition: slide-left
level: 2
---

# Сценарий - денежный перевод (плохой)
Пошаговое и прямое использование API сервисов

<img src="/money_exchange_bad.png" class="h-full rounded shadow" />

---
transition: slide-left
level: 2
---

# Сценарий - денежный перевод (плохой)

<br>

- 📝 **Бизнес логика внутри канального мобильного приложения**
- 🎯 **Завершенные шаги не сохраняются**
- 🧑‍💻 **Множественные сетевые запросы**
- 🧑‍💻 **Сложная обработка ошибок**


---
transition: slide-left
level: 2
---

# Сценарий - денежный перевод (хороший)
Один запрос для услуги через сервисный агрегатор

<img src="/money_exchange_good.png" class="h-full rounded shadow" />

---
transition: slide-left
level: 2
---

# Сценарий - денежный перевод (хороший)

<br>

- 📝 **Бизнес логика внутри service aggregator-а может быть переиспользована**
- 🎯 **Сохранение завершенных шагов**
- 🧑‍💻 **Множественные сетевые запросы эффективно обрабатываются в приватной сети**
- 🧑‍💻 **Обработка ошибок в одном месте**

---
transition: slide-left
level: 2
---

# Безопасность и приватность

<br>

## Сценарий - API для бухгалтерского учета

<br>

- 📝 **Клиент** - использует услугу по получению финансовой информации аккаунта
- 🎯 **Сервис** - предоставляет все данные в открытом виде
- 🧑‍💻 **Процедура** - фильтрация личных данных в канальном приложении

---
transition: slide-left
level: 2
---

# Сценарий - API для бухгалтерского учета (плохой)
Работа с персональными и важными данными напрямую в канальном приложении

<img src="/accounting_api_bad.png" class="h-full rounded shadow" />

---
transition: slide-left
level: 2
---

# Сценарий - API для бухгалтерского учета (плохой)

<br>

- 📝 **Бизнес логика внутри канального приложения**
- 🎯 **Уязвимость личных данных**

---
transition: slide-left
level: 2
---

# Сценарий - API для бухгалтерского учета (хороший)
Работа с персональными и важными данными делегированна сервису

<img src="/accounting_api_good.png" class="h-full rounded shadow" />

---
transition: slide-left
level: 2
---

# Сценарий - API для бухгалтерского учета (хороший)

<br>

- 📝 **Бизнес логика фильтрации в сервисном слое**
- 🎯 **Личные данные скрыты**

---
transition: slide-up
---

# Классическая канальная архитектура

- 📝 **Канальная архитектура** - границы и компоненты
- 🎯 **Каналы** - определение и примеры
- 🧑‍💻 **Клиенты** - определение и связь с пользователем
- 🚦 **Провайдеры** - определение и связь с сервисом
- 🎥 **Сервисы** - определение и примеры

---
transition: slide-left
level: 2
---

# Канальная архитектура - границы и компоненты

<img src="/channel_architecture_layered.png" class="h-full rounded shadow" />

---
transition: slide-left
level: 2
---

# Канальная архитектура - границы и компоненты

<img src="/channel_architecture_layered_borders.png" class="h-full rounded shadow" />

---
transition: slide-left
level: 2
---

# Границы канальной архитектуры

- 📝 **Пользовательский интерфейс** - Точка входа, для предоставления услуги, приложение или веб-сайт
- 🎯 **Сервисный слой** - Сервисы для инкапсуляции пользовательского доступа, интеграций
- 🧑‍💻 **Фасад / Service aggregator** - Композиция запросов, интерфейс для канального приложения

---
transition: slide-left
level: 2
---

# Каналы

- 📝 **Канал** - это способ предложить/предоставить и организовать обслуживание <u>клиента.</u>
- 🎯 **Канал обслуживания** - точка входа для предосталения и распространения услуги
- 🧑‍💻 **Множество каналов** - для покрытия большего числа клиентов

---
transition: slide-left
level: 2
---

# Каналы

<img src="/channel.png" class="h-full rounded shadow" />

---
transition: slide-left
level: 2
---

# Клиенты

- 📝 **Клиент** - это лицо или организация использующая сервис
- 🎯 **Клиент как программа** - иногда под клиентом подразумевается браузер, приложение
- 🧑‍💻 **Пользователь** - в программе, клиент может быть представлен в виде структуры данных

---
transition: slide-left
level: 2
---

# Клиенты

<img src="/clients.png" class="rounded shadow" />

---
transition: slide-left
level: 2
---

# Провайдеры

- 📝 **Провайдер услуги** - это сущность предоставляющая сервис, например другому сервису
- 🎯 **Провайдер и сервис** - отношения между провайдером и сервисом регулируются SLA
- 🧑‍💻 **Внутреннии и внешние** - внутреннии, как база данных, внешник - отдельные сервисы со своим API

---
transition: slide-left
level: 2
---

# Провайдеры

<img src="/provider.png" class="h-full rounded shadow" />

---
transition: slide-left
level: 2
---

# Сервисы

- 📝 **Сервис** - нечто реализующее услугу
- 🎯 **Функции** - различные функции сервиса могут быть реализованы без использования провайдера
- 🧑‍💻 **Делегирование** - различный функции делегируются другим сервисам для упрощения

---
transition: slide-left
level: 2
---

# Сервисы

<img src="/service.png" class="rounded shadow" />

<!--
Presenter note with **bold**, *italic*, and ~~striked~~ text.

Also, HTML elements are valid:
<div class="flex w-full">
  <span style="flex-grow: 1;">Left content</span>
  <span>Right content</span>
</div>
-->

---
transition: slide-left
layout: image-right
image: https://patchmanager.com/wp-content/uploads/IoT-office-1200-x-628.png
---

# Инфраструктура

- 📝 **CDN** - Доставка контента
- 🎯 **Cache** - Кеширование в "канальной архитектуре"
- 🧑‍💻 **Load Balancer** - Распределение входящего траффика

<!-- Инфраструктура и соответствующие сервисы в контексте
канальной архитектуры: CDN, Cache, Load Balancer-ы
Тема с API Gateway и BFF будет отдельно разобранна -->

---
transition: slide-left
layout: image-right
image: https://www.ipxo.com/app/uploads/2022/01/What-is-CDN-820x460.jpg
level: 2
---

# CDN - Content Delivery Network
Доставка контента

- 📝 **Изображения**
- 🧑‍💻 **Видео**
- 🎯 **Ресурсы для веб страницы**

<!-- Какой контент доставляем - 
картинки, видео, ресурсы веб сайты типа .css, .js и т.д
-->

---
transition: slide-left
level: 2
---

# CDN - Content Delivery Network
Доставка контента

<img src="/cdn.webp" class="rounded shadow" />

<!-- С помощью CDN доставка происходит быстрее - сервера локально ближе к клиенту -->

---
transition: slide-left
level: 2
---

# CDN - Content Delivery Network

<img src="/cdn_cache.png" class="h-full rounded shadow" />

<!-- CDN сервисы обладают кешированием, поэтому иногда необходимо пользоваться явной инвалидацией кеша -->

---
transition: slide-left
layout: image-right
image: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTvBhVx4ACXJRaVK9XA-kLfCWcb4YOoRNaYmw&usqp=CAU
level: 2
---

# Cache
"Быстрое" временное хранилище данных

- 📝 **Presentation Layer** - CDN, кеш браузера, пользовательский кеш
- 🧑‍💻 **Application Layer** - кеширование запросов
- 🎯 **Domain Layer Caching** - кеширование бд, сторонних сервисов

<!-- Кеш - быстрое хранилище данных, для быстрого доступа к часто используемым данным
Кеширование как паттерн/практика может быть применена почти к любой части системы/слою
-->

---
transition: slide-left
level: 2
---

# Cache

<img src="/caching_layers.png" class="h-full rounded shadow" />

---
transition: slide-left
level: 2
---

# Cache

- 📝 **Client Side** - Данные кешируются на стороне пользователя, например в браузере
- 🧑‍💻 **Server Side** - Данные кешируются в компонентах обрабатывающих и создающих данные

<br>

<img src="/caching_types.png" class="rounded shadow" />

---
transition: slide-left
level: 2
---

# Presentation Layer Caching

- 📝 **HTTP Caching** - Кеширование HTTP запросов к ресурсам в браузере
- 🧑‍💻 **Cache API** - Кеширование с помощью Cache API, ServiceWorker-ов
- 🎯 **Custom Local Cache** - Кеш с пользовательским контролем данных и инвалидацией

---
transition: slide-left
level: 2
---

# HTTP Caching

<img src="/http_caching.png" class="h-full rounded shadow" />

---
transition: slide-left
level: 2
---

# Cache API

<img src="/cache_api.svg" class="h-full bg-current rounded shadow" />

---
transition: slide-left
level: 2
---

# Custom Local Cache

<img src="/custom_local_cache.png" class="h-full rounded shadow" />

---
transition: slide-left
layout: image-right
image: https://www.ovhcloud.com/sites/default/files/styles/large_screens_1x/public/2022-04/network-illustration_load-balancer.png
level: 2
---

# Load balancer
Распределение входящего трафика

- 📝 **Точка входа** - Балансировщик это точка входа для входящего трафика с клиента, клиентских приложений
- 🧑‍💻 **L4 Балансировщик** - Оперирует на уровне L4 подключений
- 🎯 **L7 Балансировщик** - "Умный" балансировщик, с анализом типа трафика

<!-- Балансировщик - точка входа в апи для трафика приходящего 
с клиента и клиентского приложения
Бывают 2 типов - L4 на уровне адресов и L7 на уровне типа трафика, контента, кук и тд
-->

---
transition: slide-left
layout: image-right
image: https://media.licdn.com/dms/image/D4D12AQF1WsydWRR28g/article-cover_image-shrink_600_2000/0/1667051692815?e=2147483647&v=beta&t=yzA3kTHnMA4PNNEuNbVOwrLsdxHqrPnDOpoWXLTua38
level: 2
---

# Load balancer

- 📝 **Статические балансировщики** - распределение трафика без учета текущего состояния системы.
- 🧑‍💻 **Динамические балансировщики** - динамическое распределение трафика с учетом доступности и работоспособности сервера.

<!-- Статическая балансировка - без учета работы системы, годится только для первоначальной стадии
Динамическая - более сложная в настройке но учитывает работу системы и позволяет точную настройку
-->

---
transition: slide-left
level: 2
---

# Load balancer
Распределение входящего трафика

<img src="/load_balancer.png" class="h-full rounded shadow" />

<!-- Балансировщик - распределяет трафик по различным целям
бывает реализован в кач-ве устройства (hardware железка) так и програмным (nginx)
-->

---
transition: slide-left
level: 2
---

# Load balancer
Без балансировки трафика

<img src="/without_load_balancer.png" class="h-full bg-current rounded shadow" />

<!-- Отсутствие балансировки приводит к простоям 
одних серверов и перегруженности других
-->

---
transition: slide-left
level: 2
---

# Load balancer
С балансировкой трафика

<img src="/with_load_balancer.png" class="h-full bg-current rounded shadow" />

<!-- Наличие балансировки равномерно загружает сервера работой
-->

---
transition: slide-left
level: 2
---

# Load balancer и API Gateway

<div>API Gateway может выполнять балансировку траффика или находится перед балансировщиком</div>

<img src="/load_balancer_api_gateway.png" class="h-full bg-current rounded shadow" />

<!-- API Gateway может в балансировку!
или находится перед балансировщиками (тогда возможно нет смысла использовать балансеры типа L7)
-->

---
transition: slide-left
level: 2
---

# Load balancer SaaS/PaaS

- 📝 **Amazon ELB**
- 🧑‍💻 **Azure LoadBalancer**
- 🎯 **GCP Cloud Load Balancing**

<br>

<img src="/load_balancer_elb.png" class="bg-current rounded shadow" />

<!-- Сервисы балансировщики есть у облачных провайдеров
-->

---
transition: slide-left
level: 2
---

# Software Load balancer

<img src="/software_load_balancer.png" class="h-full bg-current rounded shadow" />

<!-- Kong - популярный api gateway с функциями балансера
-->

---
transition: slide-left
level: 2
---

# Load balancer (Orchestration)

<img src="/k8s_load_balancer.webp" class="bg-current rounded shadow" />

<!-- Различные инструменты оркестрации имеют свои тулзы для балансировки
-->

---
preload: false
---

# Пользовательский доступ

Animations are powered by [@vueuse/motion](https://motion.vueuse.org/).

```html
<div
  v-motion
  :initial="{ x: -80 }"
  :enter="{ x: 0 }">
  Slidev
</div>
```

<div class="w-60 relative mt-6">
  <div class="relative w-40 h-40">
    <img
      v-motion
      :initial="{ x: 800, y: -100, scale: 1.5, rotate: -50 }"
      :enter="final"
      class="absolute top-0 left-0 right-0 bottom-0"
      src="https://sli.dev/logo-square.png"
      alt=""
    />
    <img
      v-motion
      :initial="{ y: 500, x: -100, scale: 2 }"
      :enter="final"
      class="absolute top-0 left-0 right-0 bottom-0"
      src="https://sli.dev/logo-circle.png"
      alt=""
    />
    <img
      v-motion
      :initial="{ x: 600, y: 400, scale: 2, rotate: 100 }"
      :enter="final"
      class="absolute top-0 left-0 right-0 bottom-0"
      src="https://sli.dev/logo-triangle.png"
      alt=""
    />
  </div>

  <div
    class="text-5xl absolute top-14 left-40 text-[#2B90B6] -z-1"
    v-motion
    :initial="{ x: -80, opacity: 0}"
    :enter="{ x: 0, opacity: 1, transition: { delay: 2000, duration: 1000 } }">
    Slidev
  </div>
</div>

<!-- vue script setup scripts can be directly used in markdown, and will only affects current page -->
<script setup lang="ts">
const final = {
  x: 0,
  y: 0,
  rotate: 0,
  scale: 1,
  transition: {
    type: 'spring',
    damping: 10,
    stiffness: 20,
    mass: 2
  }
}
</script>

<div
  v-motion
  :initial="{ x:35, y: 40, opacity: 0}"
  :enter="{ y: 0, opacity: 1, transition: { delay: 3500 } }">

[Learn More](https://sli.dev/guide/animations.html#motion)

</div>

---

# Пользовательская сессия

LaTeX is supported out-of-box powered by [KaTeX](https://katex.org/).

<br>

Inline $\sqrt{3x-1}+(1+x)^2$

Block
$$ {1|3|all}
\begin{array}{c}

\nabla \times \vec{\mathbf{B}} -\, \frac1c\, \frac{\partial\vec{\mathbf{E}}}{\partial t} &
= \frac{4\pi}{c}\vec{\mathbf{j}}    \nabla \cdot \vec{\mathbf{E}} & = 4 \pi \rho \\

\nabla \times \vec{\mathbf{E}}\, +\, \frac1c\, \frac{\partial\vec{\mathbf{B}}}{\partial t} & = \vec{\mathbf{0}} \\

\nabla \cdot \vec{\mathbf{B}} & = 0

\end{array}
$$

<br>

[Learn more](https://sli.dev/guide/syntax#latex)

---

# Организация API

You can create diagrams / graphs from textual descriptions, directly in your Markdown.

<div class="grid grid-cols-4 gap-5 pt-4 -mb-6">

```mermaid {scale: 0.5, alt: 'A simple sequence diagram'}
sequenceDiagram
    Alice->John: Hello John, how are you?
    Note over Alice,John: A typical interaction
```

```mermaid {theme: 'neutral', scale: 0.8}
graph TD
B[Text] --> C{Decision}
C -->|One| D[Result 1]
C -->|Two| E[Result 2]
```

```mermaid
mindmap
  root((mindmap))
    Origins
      Long history
      ::icon(fa fa-book)
      Popularisation
        British popular psychology author Tony Buzan
    Research
      On effectivness<br/>and features
      On Automatic creation
        Uses
            Creative techniques
            Strategic planning
            Argument mapping
    Tools
      Pen and paper
      Mermaid
```

```plantuml {scale: 0.7}
@startuml

package "Some Group" {
  HTTP - [First Component]
  [Another Component]
}

node "Other Groups" {
  FTP - [Second Component]
  [First Component] --> FTP
}

cloud {
  [Example 1]
}

database "MySql" {
  folder "This is my folder" {
    [Folder 3]
  }
  frame "Foo" {
    [Frame 4]
  }
}

[Another Component] --> [Example 1]
[Example 1] --> [Folder 3]
[Folder 3] --> [Frame 4]

@enduml
```

</div>

[Learn More](https://sli.dev/guide/syntax.html#diagrams)

---
layout: center
class: text-center
---

# Backend For Frontend

[Documentations](https://sli.dev) · [GitHub](https://github.com/slidevjs/slidev) · [Showcases](https://sli.dev/showcases.html)

---
layout: center
class: text-center
---

# API Gateway

[Documentations](https://sli.dev) · [GitHub](https://github.com/slidevjs/slidev) · [Showcases](https://sli.dev/showcases.html)
