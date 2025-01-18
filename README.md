# Что здесь происходит?  
Я делаю экосистему проектов, демонстрирующую полный цикл разработки и эксплуатации современного веб-приложения:  
1. **Основное приложение — ephemerex**, обеспечивает создание и хранение "секретных сообщений", которые уничтожаются после прочтения. Прямо "как в фильмах":)  
2. Для **оценки производительности** приложения реализован **фреймворк нагрузочного тестирования** (load-forge) с использованием k6, который помогает убедиться, что приложения устойчиво к высоким нагрузкам.  
3. Задействуется Kubernetes и Harbor для **контейнеризации и оркестрации инфраструктуры**.  
4. Функциональные е2е тесты на pytest позволяют убедиться в корректности работы приложения после доработок.  
  
Все это вместе призвано резюмировать мои навыки в разработке, тестировании и развертывании комплексных систем, а так же послужить реалистичным полигоном для экспериментов и обучения:)  
  
### Роадмап  
В качестве развития планируется:  
1) Поднять harbor, хранить в нем все образы, необходимые для запуска инфраструктуры приложения  
2) Переехать в kubernetes, настроить автоскейлинг при нагрузке  
3) Проект функциональных е2е тестов с использованием pytest  
  
## ephemerex  
Сервис отправки секретных сообщений, самоуничтожающихся после прочтения. Аналог https://privnote.com/  
https://github.com/antonnneo/ephemerEx  
Написан на Python-фреймворке FastAPI.  
Использует PostgreSQL в качестве базы данных.  
Есть простой фронт и работоспособный swagger.  
Поднимается через docker compose, имеет балансировщик нагрузки и несколько инстансов приложения под ним.  
  
## load-forge  
Фреймворк нагрузочного тестирования, предназначенный для проведения НТ сервиса ephemerex  
https://github.com/antonnneo/load-forge  
Написан с использованием инструмента grafana/k6.  
В docker compose поднимается prometheus и grafana.  
Фреймворк отправляет метрики нагрузочного тестирования в prometheus, а в grafana их визуализирует специальный дэшборд.  
