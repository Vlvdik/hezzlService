# TASK #3

---

**Вопрос 1**. Почему описанная выше схема не сработает? Опишите какой будет сценарий

***Ответ***: Исходя из контекста задачи, не до конца понял, делается ли роллбэк при неудачно прошедшей транзакции. Но думаю, суть в FOR UPDATE, который лочит доступ выбранным в DB запросе полям таблицы. Когда к нам часто начнет стучаться один и тот же пользователь много раз (а с ```POST game/v1/campaignId:int/buy-crystals``` это будет сделать не трудно) и в течении короткого промежутка времени, будет неприятно. По сути, пользователь начнет вставать в очередь.

---

**Вопрос 2**. Как защитить себя от паралельных одинаковых запросов из игры? по сути от фрода

***Ответ***: По возможности, ходим в кэш, а не в базу, на примере с одинаковыми запросами это особенно актуально, стараемся следить за действиям пользователей, выдаем таймауты и т.д.

---

**Вопрос 3**. Какие могут быть последствия от параллельных запросов из игры? Например, один пользователь отправит одновременно 1000 запросов

***Ответ***: Запросы начнут отваливаться и клиент получит 5XX код ответа (на самом деле код может быть не обязательно из 5ХХ), а серверу будет больно выдерживать такой поток (если впринципе выдержит). Возможна потеря данных.