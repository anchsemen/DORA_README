# **Дизайн ML системы – DORA**
*Шаблон ML System Design Doc от телеграм-канала [Reliable ML](https://t.me/reliable_ml)*
- Рекомендации по процессу заполнения документа (workflow) - [здесь](https://github.com/IrinaGoloshchapova/ml_system_design_doc_ru/blob/main/ML_System_Design_Doc_Workflow.md).
- Детальный доклад о том, что такое ML System Design Doc и о том, как, когда и зачем его составлять - [тут](https://www.youtube.com/watch?v=PW9TGNr1Vqk).

### **1. Цели и предпосылки** 
#### **1.1. Зачем идем в разработку продукта?**  
#### **Бизнес цели**

1) Релизнуть модуль “Партнер” в телеграм-боте и доработать промты (т.е. сделать диалог качественным для пользователя) за следующие 3 месяца, также внедрить систему подписки для данного модуля. 

    **Какие методы будут использоваться для достижения цели?**
    Разработка модуля и релиз. Тестирование и исправление багов. 

2) Сформировать воронку привлечения пользователей на модуль “Партнер” за следующие 6 месяцев, и привлечь 5.000 пользователей. 

    **Какие методы будут использоваться для достижения цели?**
    Создание “банка гипотез” тестируя которые мы будем привлекать пользователей. 

3) В течение 5 месяцев монетизировать пользователей, путем введения подписочной системы за “PRO-контент” в модуле “Партнер”. 

    **Какие методы будут использоваться для достижения цели?**
    CustDev с пользователями и выявление паттернов (шаблонов) поведения, результатами которых будет покупка подписки на бота.


#### **Почему станет лучше, чем сейчас, от использования ML**
На данный момент проблема, которую мы решаем с применением технологий ML, решается использованием личного общения и тратой большего количества денег и человеческих часов. 

Рассмотрим пример: Есть Максим, и у него сложности с общением и социализацией, возникшие из-за удаленной работы и из-за того, что у него маленькое окружение для общения и есть сложности с восприятием себя (слишком завышенная самооценка). 


Решение проблем со стороны Максима: 
1. Походы к психологу (4.000 ₽/прием)
2. Постоянное общение с другом
3. Постоянное общение с девушками в приложениях для знакомств (≈ 700 ₽/неделя)

Для друга Максима постоянная поддержка, которую он дает Максиму дается тяжело, потому что это требует много сил и внимания, и поэтому для него периодами становится это тяжело.

**Как решит бот все эти проблемы:** 
1. Поддержка и общение
2. Партнер
3. И он всегда на связи, всегда можно поговорить и написать, буквально о самых простых бытовых вещах. 
И решая все проблемы убирается человеческих фактор, бот заменяет 3-5 людей из окружения пользователя.


#### **Что будем считать успехом итерации с точки зрения бизнеса** 
1. Выполнение поставленных целей, а если не выйдет их реализовать, то анализ нашего опыта и проделанной работы и понимание, какие мы ошибки мы допустили.
2. Запуск системы подписок в боте, и поиск пользователей, которые будут платить.
3. CustDev платящих пользователей. 
4. формирование дальнейших планов по развитию продукта.



#### **1.2. Бизнес-требования и ограничения**
#### **Краткое описание БТ и ссылки на детальные документы с бизнес-требованиями**

**Функциональные требования:**
1. Интерактивное взаимодействие: бот должен способствовать непринужденному и естественному общению с пользователем, предлагая ответы на вопросы, предоставляя информацию или просто развлекая. При общении с ботом у пользователя должно складываться впечатление будто он общается со своим хорошим другом или близким человеком. 

2. Распознавание речи и текста, распознавание и запоминание контекста:
    - бот должен уметь распознавать сообщения пользователя и выстраивать диалоговую линию; 
    - бот должен уметь распознавать голосовые сообщения от пользователя.


3. Персонализированный опыт: бот должен учитывать предпочтения и интересы пользователя, предоставляя контент, который наиболее подходит для конкретного человека.

**Нефункциональные требования:**
1. Безопасность данных: бот должен гарантировать защиту конфиденциальности и безопасность информации, предоставляемой или получаемой от пользователя.

2. Скорость ответа: бот должен обеспечивать низкую задержку при ответах бота для создания естественного и плавного взаимодействия.

3. Доступность: гарантировать, что бот доступен для пользователей в течение большей части времени.

4. Масштабируемость: обеспечить способность бота обрабатывать увеличивающееся количество пользователей, сохраняя при этом высокий уровень производительности.

**Требования к контенту:**
1. Разнообразие контента: бот должен обеспечить наличие разнообразного контента, который может быть предоставлен пользователю, включая полезную информацию, ролевые игры и другие развлекательные элементы, общение в формате 18+. 

2. Обновление контента: регулярное обновление бота для улучшения общения с пользователями.

#### **Бизнес-ограничения** 
**1. Ограничения по безопасности данных:**
Бот должен соблюдать стандарты безопасности данных и предоставлять гарантии отсутствия утечек личной информации пользователя. Необходимо также обеспечить шифрование данных для защиты конфиденциальности.

**2. Ограничения по контенту:**
Бот должен следовать правилам и стандартам в отношении контента, с учетом законодательства. При общении с ботом пользователи должны ознакомиться с политикой конфиденциальности и Правилами пользования, а при покупке подписки с офертой.

**3. Ограничения по обучению модели:** 
Процесс обучения модели бота должен не допускать обучение на данных, нарушающих правила конфиденциальности. Обучение модели должно строиться на открытых датасетах и на данных со свободной лицензией пользования.

**4. Ограничения по интеграции с другим ПО:**
Бот может столкнуться с ограничениями в интеграции с другим ПО, так как исходный код бота и используемые библиотеки могут быть несовместимы с определенными технологиями или стандартами.

**5. Ограничения по доступности:**
Бот может сталкиваться с ограничениями в обеспечении высокой доступности и скорости, так как это зависит от стабильности и доступности используемых открытых моделей.

**6. Ограничения по локализации и языковой поддержке:**
Бот может оказывать ограниченную поддержку различных языков и культур, из-за языковых особенностей в разных странах. Необходимо ясно определить доступные языки и уровень поддержки.

**7. Соблюдение лицензионных ограничений:** 
Бот должен строго соблюдать условия лицензий, предоставленных открытыми моделями в опенсорсе, которые будут использоваться в боте, и не противоречить ограничениям, установленным правообладателями.

**8. Контроль за этическими аспектами:**
Бот должен соблюдать этические стандарты, не пропагандировать негативное поведение или дискриминацию, и обеспечивать этическое взаимодействие с пользователями.

**9. Оказание психологической помощи:** 
При использовании бота до пользователей перед использованием необходимо донести информацию о том, что бот не является медицинским специалистом и не оказывает психологическую помощь, а только поддерживает (помогает) как друг и/или близкий человек. 

**10. Ограничение серверных мощностей для работы нейронных сетей:** 
Ограничение по серверным мощностям связано с необходимостью обеспечения достаточных вычислительных ресурсов для эффективного функционирования нейронных сетей, используемых в боте.



#### **Что мы ожидаем от конкретной итерации?**
Чтобы спрогнозировать цели, которые будут ожидаться от итерации необходимо поставить сроки для одного итеративного цикла. Ближайший итеративный цикл ставится на январь: 
|**Срок**|**Проводимые работы**|**Результат**|
| :-: | :-: | :-: |
|Январь|Реализация модуля “Партнер” в боте, которая включает в себя:  <ol><li>дообучение модели на датасетах</li><li>интеграция модели в бота</li><li>создание библиотеки с персонажами для модуля</li><li>тестирование диалогов</li><li>промпт-инжиниринг и создание ветвей диалогов</li></ol> | Готовый модуль “Партнер”, интегрированный в бота в телеграмме, в котором у пользователя будет возможность: <ol><li>выбора персонажа</li><li>общение с персонажем в рамках заданного модуля</li><li>общение в рамках диалогов с контентом 18+</li></ol>|

#### **Описание бизнес-процесса пилота, насколько это возможно.** 
На данным этапе проекта, мы может составить описание бизнес-процесса, и ожидаемые результаты по итогам выполнения. Пилот проекта — это разработка модуля “Партнер” и его релиз в существующего бота, привлечение пользователей и формирование сообщества этих пользователей. Описание бизнес-процесса пилота представлено в таблице: 

Пояснение: в данной таблице приведено описание для итерации разработки, запланированной на январь. Если мы рассматриваем вопрос с привлечением пользователей — то мы говорим об итерации с января по март (включительно).

|**Шаги процесса:**|**Описание:**|
| :-: | :-: |
|Определение точки старта и точки завершения|Точка старта: <br> 1) Чат-бот с модулем “Поддержка” в телеграме. 2) 280 пользователей. 3) Готовый сайт проекта. <br> Точка завершения: <br> <ol><li>Готовый модуль “Партнер”, который интегрирован в существующего чат-бота.</li><li>Улучшенный модуль “Поддержка”.</li><li>Заложено начало для формирование воронки для привлечения пользователей в модуль “Партнер”.</li><li>Привлечено около 5.000 пользователей в модуль "Партнер"</li><li>Собрана обратная связь от пользователей и более глубоко сегментирована ЦА.</li></ol>|
|Роли и ответственности|Семен Кирсанов — CTO, ML-разработчик, Backend-разработчик <br> Слава Чупринова — Product Owner, CEO <br> ??? — контент-креатор, пока в поисках|
|Технологические и информационные требования|**Технологические требования:** <br> <ol><li>Серверные мощности для работы нейронных сетей</li><li>Датасеты или библиотеки, которые служат основой для обучения нейронных сетей, лежащих в основе бота.</li></ol> <br> **Информационные требования:** <br> <ol><li>Логика взаимодействия пользователя с ботом, которая включает продуманные сценарии.</li><li>Хранение данных о пользователях: продумывание вопроса конфиденциальности и безопасности данных, продумывание Пользовательских соглашений и Политики конфиденциальности (к реализации данного вопроса привлечен юрист, который занимается данным вопросом).</li></ol>|
|Критерии оценки успеха|Оценка успеха будет определяться по: <br> <ol><li>Качеству ответов бота при общении с пользователями, наличию артефактов в ответах.</li><li>Количеству привлеченных пользователей.</li><li>Процентному соотношению платящих пользователей к не платящим, и переходу пользователей из первой категории во вторую.</li></ol> |
|Ожидаемый результат|Выполнен план по запуску пилота и собрана обратная связь от пользователей, выявлены точки роста, поставлен спринт для следующей итерации проекта|
|План тестирования и доработки продукта|<ol><li>Релиз модуля “Партнер” в готового чат-бота и подключение небольшой группы пользователей к тестированию модуля.</li><li>Сбор обратной связи от пользователей.</li><li>Выявление ошибок на основе ОС от пользователей и составление плана по устранению ошибок и возможным улучшениям.</li><li>Устранение ошибок и доработка модуля в боте.</li><li>Тестирование допустимой нагрузки.</li><li>Релиз модуля для всех пользователей.</li></ol>|
|Выявление точек роста/масштабирования|<ol><li>Анализ поведения пользователей при взаимодействии с ботом, нахождение мест, где пользователи “отваливаются”, “теряют интерес”.</li><li>Анализ пользователей из которых состоит сформированное “сообщество”.</li><li>Создание “банка гипотез” по дальнейшему развитию.</li></ol>| 

#### **Что считаем успешным пилотом? Критерии успеха и возможные пути развития проекта**
Успешным пилотом для ближайшей итерации (описана в предыдущих пунктах) считается: 
1. Разработка модуля “Партнер” и интеграция его в существующего бота; 
2. Привлечение новых пользователей; 
3. Сбор и анализ обратной связи от пользователей; 
4. Выявление точек роста и постановка нового спринта.

#### **1.3. Что входит в скоуп проекта/итерации, что не входит**
В данный момент чат-бот асинхронно отвечает каждому пользователю, что при высокой нагрузке дает хорошие показатели, единственный минус - работа модели из модуля “Поддержка” - в 1 минуту модель может обработать до 60 запросов, данный момент пока не решается, но уже в поисках.

**Технический долг:** 
1. Оставляем проработку телеграм-бота
2. Возможность писать чат-боту, если пользователь подписан на информационный tg канал
3. Оформление подписки для оплаты модуля “Партнер”
4. Проработка остальных модулей

#### **1.3 Предпосылки решения**
В данный момент чат-бот запускается локально, ведется поиск сервера для полного перехода на автоматизацию. 

- Проект ведётся в Github;
- Документация – в процессе создания, будет в google doc.
- Код - в Pycharm, соответствует PEP8, разбит на модули
- Стек - Aiogram, Transformers, OpenAI
- БД -  Firebase/MongoDB

### **2. Методология**
#### **2.1 Постановка задачи**
Создание генеративного чат-бота с различными модулями общения (поддержка, партнер, проработка общения, знаменитость)

#### **2.2 Блок-схема решения**
Файл блок-схема.jpeg

#### **2.3 Этапы решения задачи**

### **3. Подготовка пилота**
#### **3.1 Способ оценки пилота**
#### **Краткое описание предполагаемого дизайна и способа оценки пилота**
Пилот представляет из себя чат-бота, у которого есть такие функции как: 
1. Выбор персонажа из библиотеки персонажей. 
2. “Библиотека персонажей” представляет из себя карточки персонажей с их фотографиями и описание (превью).

   **Примеры персонажей**

   **Девушка. Кайли.**


   <img src=Кайли.jpeg>


   **Описание:** Солнечная мулатка, словно воплощение летнего света и тепла. Ее смешанный цвет кожи, темные глаза и кудрявые волосы создают чарующий облик. Естественная красота, выраженная индивидуальность и теплый, приветливый взгляд делают ее привлекательной и непосредственной. Кайли излучает свет, наполняя окружающих яркими красками и позитивной энергией. 

   **Парень. Марк.**

   
 <img src=Марк.png>

 
   **Описание:** Взгляд Марка, обладающего тонким интеллектом, словно загадочный луч света, притягивает внимание своей остротой. Его внешность, стильная прическа и ухоженная борода придают ему особую атмосферу утонченности и легкой загадочности, как будто он только что сошел со страниц детективного романа.

4. Модули “Поддержка” и модуль “Партнер”, интегрированные в бота. Продуманные диалоговые линии. 

5. Распознавание ботом текстовых и голосовых сообщений, запоминание информации о пользователе и использование её в диалоге. 

6. Отправка пользователю фотографий со стороны бота, подходящий под контекст диалога. 

#### **3.2. Что считаем успешным пилотом**
**Успешный пилот в рамках ближайшей итерации состоит из:** 
1. Готового модуля “партнер”, который интегрирован в существующего чат-бота.
2. Улучшенного модуля “поддержки” и релиз его в существующего бота. 
3. Заложено начало для формирование воронки для привлечения пользователей в модуль “партнер”.
4. Привлечено около 5.000 пользователей в модуль партнер 
5. Собрана обратная связь от пользователей и более глубинно сегментирована ЦА.


**Формализованные в пилоте метрики оценки успешности**
1. Качество ответов, диалога чат-бота с пользователями: качественность диалогов, возвращаемость пользователей к боту. 
2. Персонализированность бота: насколько бот запоминает вводные данные и учитывает их при общении с пользователем (делает упоминания, ссылается). 
3. Качество контента: отправляет ли бот фото, присутствуют ли артефакты на фото. 
4. Анализ гипотезы по привлечению пользователей: какие из гипотез работают эффективно, а какие нет; качественность постановки гипотез. 
5. Метрика по росту пользователей: какие каналы работают; через какой трафик были привлечены; конверсия неплатящих в платящих пользователей; возвращаемость пользователей; на каких этапах мы теряем пользователей при переходе их продукт. 
