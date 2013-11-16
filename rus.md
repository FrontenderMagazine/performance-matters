# Производительность имеет значение

> **Примечание от редакторов A List Apart:** В каждом выпуске один из авторов 
W3C будет вводить вас в курс дела над чем мы работаем и как в этом можно 
поучаствовать. В этом месяце колонку ведёт Ятиндер Манн (Jatinder Mann), 
руководитель проекта Internet Explorer и редактор Рабочей группы W3C по 
веб-производительности. Ятиндер хотел бы поблагодарить сопредседателей по 
рабочей группе, Арвинда Джайна (Arvind Jain) и Джейсона Вебера (Jason Weber), а 
также Филиппа Ле Хегаре за вклад в статью.

Может лет десять назад и считалось нормальным пойти заварить себе кофе пока 
загружается компьютер, однако сегодня мы рассчитываем на быстроту и отзывчивость 
программ и устройств. То же касается и веб-производительности. Быстрота загрузки 
и отзывчивость играют критическую роль в нашем выборе какими веб-приложениями 
пользоваться. В то же время, эффективность приложения значительно влияет на 
продолжительность жизни батареи устройства. Никто не хочет таскать за собой 
устройство напоминающее кирпич. 

Чтобы создавать быстрые веб-приложения, веб-разработчики нуждаются в возможности 
качественно измерять производительность приложения, эффективно использовать 
аппаратные ресурсы и, что наиболее важно, определять какие решения нужно 
оптимизировать, а от каких отказаться вообще. 

Мы обнаружили что разработчикам не доступны соответствующие инструменты. Им 
остаётся работать, полагаясь на догадки, как результат в большинстве случаев 
веб-разработчики уделяют внимание производительности JavaScript и приравнивают 
её к веб-производительности.

Однако веб-производительность — это поистине многоплановое явление. Насколько 
быстро подключение к сети позволяет загрузить ресурсы, насколько эффективно 
процессор может выполнять динамические операции в сети, количество доступной 
графической памяти — это всё влияет на веб-производительность. Давайте подробнее 
рассмотрим пример, который я привел в презентации на конференции [Build][1]; в 
нём за основу взяты пять реально существующих веб-приложений для бронирования 
туристических туров: Kayak, Expedia, Priceline, Travelocity, и Orbitz. На 
страницах всех этих сайтов размещены очень похожие элементы. У них всех есть 
логотипы, баннерная реклама, интерактивная информация о полётах, обновляемая в 
режиме реального времени, и т.д. Можно было бы предположить, что у них всех 
примерно одинаковые показатели производительности. 

На рисунке 1 представлены показатели для каждого из этих сайтов, без указания 
названия сайтов (тыкать в кого-то пальцами нам ни к чему). Как видите, хоть у 
всех этих туристических сайтов схожие функции, их дизайн сильно отличается. У 
некоторых акцент приходится на передачу ресурсов, другие более загружены кодом 
JavaScript.

<table>
<tr><th></th><th>Общий размер (тыс.)</th><th>Количество элементов</th><th>CSS-правила</th><th>Файлы изображений</th><th>Строки скрипта</th></tr>
<tr><td>Сайт №1</td><td>3,697</td><td>1,504</td><td>1,392</td><td>41</td><td>77,768</td></tr>
<tr><td>Сайт №2</td><td>2,278</td><td>1,100</td><td>5,325</td><td>29</td><td>39,183</td></tr>
<tr><td>Сайт №3</td><td>1,061</td><td>2,673</td><td>1,105</td><td>66</td><td>12,643</td></tr>
<tr><td>Сайт №4</td><td>1,812</td><td>4,252</td><td>1,672</td><td>12</td><td>10,284</td></tr>
<tr><td>Сайт №5</td><td>1,372</td><td>900</td><td>3,902</td><td>6</td><td>38,269</td></tr>
</table>

Многие разработчики могут предположить что наиболее быстрым должен быть сайт с 
наименьшим количеством форматных строк JavaScript, как Сайт №4, или же тот, для 
которого скачивается наименьшее количество байтов, как Сайт №3. Однако, это не 
так. На самом деле самый быстрый  — Сайт №5, хотя у него больше JavaScript-кода 
и скачиваемых байтов. На рисунке 2 показано сколько времени у каждого из этих 
сайтов уходит на различные подсистемы браузеров — подсистемы, которые есть у 
каждого веб-браузера, основанного на стандартах.

![диаграмма][Столбчатая диаграмма, демонстрирующая время загрузки каждой подсистемы браузера в миллисекундах для пяти сайтов]

*Время, которое уходит на подсистемы браузера для загрузки пяти наиболее 
популярных туристических сайтов.*

В действительности здесь есть два момента. Важно не только чтобы JavaScript 
выполнялся наиболее эффективно, но и чтобы все подсистемы браузера могли 
работать вместе наиболее продуктивно. Не имея в наличии надлежащих инструментов, 
разработчики не могут узнать, почему их приложения медлительны и что нужно 
оптимизировать.

Большинство веб-экспертов пришло к заключению, что разработчики нуждаются в 
более эффективных интерфейсах для измерения параметров приложений и написания 
более быстрого кода. Более того, есть необходимость в организации собрания, на 
котором можно было бы обсудить проблемы производительности, с которыми 
столкнулись разработчики, и методы их решения.

Такие люди, как Стив Саундерс (Steve Souders) и Арвинд Джайн из Google, Джейсон 
Вебер из Microsoft, Джейсон Собель (Jason Sobel) из Facebook, и др. приступили 
на технических конференциях к обсуждению вопросов, связанных с 
производительностью, таких как реализация точного и межоперационного способа 
измерения времени операций для загрузки страниц. Это обсуждение вскоре привело к 
формированию рабочей группы в консорциуме W3C, сосредоточенной исключительно на 
производительности. Летом 2010 года Джейсон Вебер из Microsoft и Арвинд Джайн из 
Google были выбраны сопредседателями новоиспечённой Рабочей группы W3C по 
производительности, созданной для идентификации и решения проблем 
производительности, с которыми столкнулись разработчики в сети.

Не все верили, что эти сотрудники конкурирующих структур смогут работать вместе. 
Первым комментарием к [посту][2] в блоге IE Blog, посвящённом созданию рабочей 
группы, в отношении к сопредседательству Google и Microsoft было замечание: 
«Готов поспорить, что шкала Рихтера могла бы уловить сейсмическую активность в 
комнате, где это произошло». Быстрая перемотка вперёд, в 2013 год (проигнорируем 
тот факт, что шкала Рихтера не является физическим инструментом сейсмической 
активности) и, как видим, Рабочая группа по производительности стала образцом 
идеальной рабочей группы. Всего за три года представители Microsoft, Google, 
Mozilla, Intel, DynaTrace и других компаний в этой группе создали ряд API, 
которые позволяют разработчикам измерять параметры веб-приложений более точно и 
достоверно чем когда либо (спецификации [Время загрузки страницы (Navigation 
Timing)][3], [Время загрузки ресурсов (Resource Timing)][4], [Пользовательское 
время (User Timing)][5], [Хронология продуктивности (Performance Timeline)][6], 
[Высокая разрешающая способность по времени (High Resolution Time)][7]) и более 
эффективно планировать операции в веб-приложениях ([`requestAnimationFrame`][8], 
[Видимость страницы (Page Visibility)][9], [Создание эффективного скрипта 
(Efficient Script Yielding)][10]). Исходя из обсуждений на Семинаре W3C по 
веб-производительности, который был организован рабочей группой чтобы услышать 
доклады 45 экспертов в области производительности и веб-разработчиков из 21 
организации, на данный момент рабочая группа проводит активную работу над шестью 
новыми спецификациями, призванными решить другие проблемы производительности: 
эффективное назначение приоритетов при загрузке ресурсов ([Приоритетность 
ресурсов (Resource Priorities)][12]), асинхронная передача данных без блокировки 
выгрузки страницы ([Beacon][13]), получение подробного отчёта о сетевых ошибках 
и подключении ([Сбор данных об ошибках навигации (Navigation Error Logging)][14], 
[Сбор ошибок при загрузке ресурсов (Resource Error Logging)][15]), маркировка 
ссылок для немедленной загрузки (предварительная генерация) и улучшение 
существующих интерфейсов ( [Время загрузки страницы 2 уровень(Navigation Timing 
L2)][16], [Высокая разрешающая способность по времени 2 уровень (High Resolution 
Time L2)][17]). Всего лишь за 11 месяцев спецификация Высокая разрешающая 
способность по времени прошла путь от идеи до полной реализации во всех ведущих 
браузерах и была признана стандартом. Это своего рода рекорд!

Оглядываясь назад, можно утверждать, что консорциум W3C стал идеальной основой 
для собрания разработчиков ведущих браузеров, веб-разработчиков и экспертов в 
области производительности для обсуждения и попытки решить главные проблемы 
производительности. Когда веб-разработчики начнут писать более эффективные 
веб-приложения и разработчики браузеров создадут среду выполнения, которая 
сможет удовлетворить требования этих веб-приложений, мы все сможем наслаждаться 
более быстрым и отзывчивым просмотром веб-страниц. 

Планы W3C не ограничиваются Рабочей группой по веб-производительности, в них 
также входит сотрудничество со специалистами с целью улучшения браузеров, 
разработки инструментов, образовательных работ и продвижения производительности 
в спецификациях W3C.

Не будем останавливаться на достигнутом. Присоединяйтесь к обсуждению вопросов 
производительности в Рабочей группе по веб-производительности!

[1]: http://channel9.msdn.com/Events/Build/2012/3-132
[2]: http://blogs.msdn.com/b/ie/archive/2010/08/18/microsoft-to-co-chair-new-w3c-web-performance-working-group.aspx
[3]: http://www.w3.org/TR/2012/REC-navigation-timing-20121217/
[4]: http://www.w3.org/TR/2012/CR-resource-timing-20120522/
[5]: http://www.w3.org/TR/2012/CR-user-timing-20120726/
[6]: http://www.w3.org/TR/2012/CR-performance-timeline-20120726/
[7]: http://www.w3.org/TR/hr-time/
[8]: http://www.w3.org/TR/animation-timing/
[9]: http://www.w3.org/TR/page-visibility/
[10]: https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/setImmediate/Overview.html
[11]: http://www.w3.org/2012/11/performance-workshop/
[12]: https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/ResourcePriorities/Overview.html
[13]: https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/Beacon/Overview.html
[14]: https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/NavigationErrorLogging/Overview.html
[15]: https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/ResourceErrorLogging/Overview.html
[16]: https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/NavigationTiming2/Overview.html
[17]: https://dvcs.w3.org/hg/webperf/raw-file/tip/specs/HighResolutionTime2/Overview.html
[18]: http://www.w3.org/2013/Talks/0610-performance/#/

[Столбчатая диаграмма, демонстрирующая время загрузки каждой подсистемы браузера в миллисекундах для пяти сайтов]: img/MannFig2_lo-ru.png