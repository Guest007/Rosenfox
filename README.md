# Rosenfox
Pure, fast and secure settings for Mozilla Firefox (about:config and user.js only). Global and complete manual.

Version 0.1.1: 2016/02/01

Version 0.1.2: 2016/02/07

Version 0.1.3: 2016/02/16

**0/ ПРЕАМБУЛА**

Задачи повышения безопасности и приватности, а также достижения должной степени анонимности с целью предотвращения возможных атак и сбора данных третьей стороной решаются, как правило, установкой сторонних дополнений в Mozilla Firefox, что отрицательно сказывается на скорости загрузки и работы браузера. Кроме того, в сторонних дополнениях не гарантируется отсутствие утечек, уязвимостей и встроенных средств несанкционированного доступа.

Данное руководство обеспечивает максимум безопасности и повышает анонимность конечного пользователя исключительно за счет внутренних настроек браузера, вызываемых через about:config.

Основной принцип, использовавшийся при составлении данного руководства:

"ЗАПРЕЩЕНО ВСЁ, ЧТО ЯВНО НЕ РАЗРЕШЕНО ПОЛЬЗОВАТЕЛЕМ!"


**Примечание 1:** В вашей версии Firefox  могут отсутствовать некоторые единичные настройки - измененные или удаленные в связи с постоянной разработкой браузера или предназначенные для мобильной версии программы (ОС Android и т.п.). Желая охватить как можно больше последних выпусков Firefox, описание таких настроек не удалено, но (по возможности) помечено специальным образом. 

**Примечание 2:** Никогда не изменяйте какие-либо настройки, если вы не понимаете, что делаете! 

**Примечание 3:** Если какая-то из конкретных настроек отсутствует в вашей версии браузера, не стремитесь внести новую строку в about:config - вполне возможно, что она там попросту не нужна. Ориентируйтесь на комментарии, приводимые в руководстве (например: "необходимо создать" и т.п.).

**Примечание 4:** В рекомендуемой конфигурации Firefox в принципе вообще нежелательно устанавливать какие-то сторонние дополнения. Помните, что их внутренние установки могут войти в конфликт с настройками, рассматриваемыми в данном руководстве, или перезаписать их!

**Примечание 5:** Рекомендуемые настройки увеличивают степень пользовательской приватности и безопасности, однако создают уникальный "цифровой отпечаток" браузера, который может способствовать уменьшению степени анонимности. Вам предоставляется право самостоятельно определять разумный баланс между приватностью/безопасностью и анонимностью.

**Примечание 6:** Внимательно изучайте действие каждой настройки. Помните, что многие из них могут привести к  снижению функциональности браузера, а именно: 

а) отсутствию изображений и запрету мультимедийного контента на веб-страницах;

б) отсутствию управляющих элементов и частичному нарушению работоспособности сайтов (особенно сделанных по Flash или JavaScript-технологиям);

в) невозможности работы с веб-ресурсами, требующими авторизации: почтовыми сервисами, форумами, социальными сетями. 

Как правило, это происходит при запрете кукиз, рефереров, перенаправлений, подделке user-agent и глобальном запрете скриптов. В этом случае мы рекомендуем создать отдельный пользовательский профиль, предназначенный исключительно для работы с надежными веб-ресурсами, внести в него остальную часть предлагаемых настроек, разрешив однако при этом скрипты, прием сеансовых кукиз, перенаправления, передачу рефереров, отображение графики и отсылку реального user-agent.

**00/ ОТКАЗ ОТ ОТВЕТСТВЕННОСТИ**

Никогда и ни при каких обстоятельствах составитель данного руководства не будет нести никакой моральной или материальной ответственности ни перед какой физической или юридической стороной за любой прямой, непрямой, особый или иной косвенный ущерб в результате любого использования приводимой информации (включая программные настройки), в том числе - за любую упущенную выгоду, приостановку деятельности, потерю данных прикладных программ или данных в операционных системах, нарушение их работоспособности, а также за нарушение пользовательской приватности или анонимности.

**000/ ЛИЦЕНЗИРОВАНИЕ И ДАЛЬНЕЙШЕЕ РАСПРОСТРАНЕНИЕ**

Настоящее руководство распространяется по свободной лицензии GNU Free Documentation License (в ее текущей версии):

http://www.gnu.org/licenses/fdl-1.3.en.html

Вся сторонняя информация, цитируемая в руководстве, почерпнута из публичных открытых источников, на которые приводятся активные ссылки.

Вы вправе свободно копировать, видоизменять и распространять данное руководство, соблюдая условия, определяемые лицензией GNU FDL; с указанием авторства составителя документа - **Rami Rosenfeld** - и активной ссылкой на проект:

**2016 Rami Rosenfeld - https://github.com/RamiRosenfeld/Rosenfox**

*Permission is granted to copy, distribute and/or modify this document under the terms of the GNU Free Documentation License, Version 1.3 or any later version published by the Free Software Foundation; with no Invariant Sections, no Front-Cover Texts, and no Back-Cover Texts.*


