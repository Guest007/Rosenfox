## I. СОЗДАНИЕ НОВОГО ПРОФИЛЯ

Используйте менеджер профилей, чтобы создать новый профиль Firefox. 

LINUX:

В терминале (консоли) Linux исполните команду от обычного пользователя:

    firefox -P

WINDOWS:

Выполните команду:

    "C:\Program Files\Mozilla Firefox\firefox.exe" -p

или (32-битная версия Firefox в 64-разрядной системе):

    "C:\Program Files (x86)\Mozilla Firefox\firefox.exe" -P

В открывшемся менеджере профилей нажмите на "Create Profile...", чтобы запустить мастер его создания. Нажмите на "Next" и выберите имя для нового профиля. Затем нажмите на "Finish".

Если менеджер профилей не запускается, скорее всего, Firefox запущен в фоновом режиме (или не закрыт). Закройте все версии Firefox или перезапустите компьютер.

https://support.mozilla.org/en-US/kb/profile-manager-create-and-remove-firefox-profiles


## II. ДОСТУП К НАСТРОЙКАМ

После запуска браузера введите about:config в адресной строке и нажмите на Enter чтобы открыть список настроек:

    about:config

http://kb.mozillazine.org/About:config


## III. ИЗМЕНЕНИЕ НАСТРОЕК

- JAVASCRIPT

JavaScript - язык программирования; одна из главных веб-технологий. В то же время JavaScript позволяет запускать вредоносный код на любом компьютере при помощи двух основных типов уязвимостей. XSS-уязвимости используются, если у атакующей стороны есть возможность внедрить исполнимый код на страницу и продемонстрировать ее пользователю. В этом случае злоумышленник может получить права данного пользователя и использовать их в своих целях. Иной тип уязвимости - CSRF, когда атакующая сторона пытается заставить браузер осуществить нежелательное действие на другом сайте, например - перевести средства со счета на счет. JavaScript-технологии могут способствовать утечкам разнообразной информации об операционной системе, браузере, размере и разрешении монитора, установленных шрифтах и других данных.

JavaScript - блокирование всех элементов: скрипты не будет запускаться глобально:

    javascript.enabled=false

http://kb.mozillazine.org/Javascript.enabled

Дополнительно: JavaScript - создание "белого списка" (white-list). Вы можете создать "белый список" сайтов, которым разрешено исполнение JavaScript вне зависимости от глобальной политики запрета их в браузере. Добавьте в файл user.js следующие строки:

    user_pref("capability.policy.policynames", "jsok");
    user_pref("capability.policy.default.javascript.enabled", "noAccess");
    user_pref("capability.policy.jsok.sites", "http://www.safe-site-1.com  https://safe-site-2.net");
    user_pref("capability.policy.jsok.javascript.enabled", "allAccess");

Примечание: Вместо "http://www.safe-site-1.com  https://safe-site-2.net" и т.п. напишите через пробел адреса необходимых "безопасных" сайтов.

http://kb.mozillazine.org/Allowing_only_certain_sites_to_use_JavaScript

Внимание: JavaScript является основной веб-технологией, приводящей к потенциальным глобальным утечкам пользовательских данных, деанонимизации и атакам на браузер и операционую систему!


- DOM (Document Object Model) STORAGE

Отключение хранилища DOM. DOM-спецификации веб-приложений определяют механизм, разрешающий веб-страницам сохранять свои данные на клиентской стороне в специальном хранилище. Хранилище необходимо отключить:

    dom.storage.enabled=false

http://kb.mozillazine.org/Dom.storage.enabled

https://en.wikipedia.org/wiki/Document_Object_Model

- DOM JavaScript

Отключение JavaScript, исполняемого с помощью DOM. Когда веб-страница загружена, браузер создает ее "модель поведения" и может позволить гипотетическое исполнение нежелательного и потенциально опасного функционала. Для предотвращения следующих действий:

а) JavaScript может добавлять, менять и удалять любые HTML-элементы и атрибуты страницы.

б) JavaScript может менять все стили CSS на странице.

в) JavaScript может реагировать на любые события на странице.

г) JavaScript может создавать новые события на странице

-необходимо активировать/деактивировать следующие функции:

Запрет скриптам скрывать окна:

    dom.allow_scripts_to_close_windows=false

Запрет скриптам разворачивать/скрывать окна:

    dom.disable_window_flip=true

Запрет скриптам менять размер/перемещать окна:

    dom.disable_window_move_resize=true

Запрет скриптам отключать кнопку закрытия окна:

    dom.disable_window_open_feature.close=true

Запрет скриптам скрывать адресную строку:

    dom.disable_window_open_feature.location=true

Запрет скриптам скрывать панель меню:

    dom.disable_window_open_feature.menubar=true

Запрет скриптам скрывать кнопку минимизации окна:

    dom.disable_window_open_feature.minimizable=true

Запрет скриптам изменять размер окна:

    dom.disable_window_open_feature.resizable=true

Запрет скриптам скрывать полосы прокрутки:

    dom.disable_window_open_feature.scrollbars=true

Запрет скриптам скрывать панель состояния:

    dom.disable_window_open_feature.status=true

Запрет скриптам скрывать личную панель:

    dom.disable_window_open_feature.personalbar=true

Запрет скриптам скрывать панель заголовка:

    dom.disable_window_open_feature.titlebar=true

Запрет скриптам скрывать панель управления:

    dom.disable_window_open_feature.toolbar=true

Мы настоятельно рекомендуем отключить дополнительный функционал DOM:

    browser.dom.window.dump.enabled=false
    dom.indexedDB.enabled=false
    dom.archivereader.enabled=false
    dom.cellbroadcast.enabled=false
    dom.event.clipboardevents.enabled=false
    dom.datastore.enabled=false
    dom.enable_performance=false
    dom.enable_resource_timing=false
    dom.fetch.enabled=false
    dom.gamepad.enabled=false
    dom.gamepad.non_standard_events.enabled=false
    dom.icc.enabled=false
    dom.identity.enabled=false
    dom.mobileconnection.enabled=false
    dom.mozAlarms.enabled=false
    dom.mozApps.used=false
    dom.mozContacts.enabled=false
    dom.mozNetworkStats.enabled=false
    dom.mozSettings.enabled=false
    dom.netinfo.enabled=false
    dom.sms.enabled=false
    dom.server-events.enabled=false
    dom.telephony.enabled=false
    dom.voicemail.enabled=false
    dom.wakelock.enabled=false
    dom.webnotifications.enabled=false


- COOKIES

Cookie - фрагмент данных (небольшой текстовый файл), отправляемый сервером и сохраняющийся в браузере. Когда пользователь вновь загружает ту же самую страницу, браузер отсылает cookie назад на сервер и уведомляет его тем самым о предыдущей активности приложения. Cookie хранят такую информацию, как пароли, логины, сеансовые данные, данные кредитных карт, электронные почтовые адреса и записывают различную пользовательскую активность и прочую статистику.

Глобальный запрет приема cookies (в том числе - со сторонних сайтов):

    network.cookie.cookieBehavior=2 (рекомендовано)

http://kb.mozillazine.org/Network.cookie.cookieBehavior

Прием cookie только с посещаемого (оригинального) сайта. Cookie со сторонних (third-party) серверов будут блокироваться:

    network.cookie.cookieBehavior=1 (не рекомендуется)

Примечание: В последнем случае (=1) необходимо активировать опцию устаревания загруженных cookies при закрытии браузера:

    network.cookie.lifetimePolicy=2

http://kb.mozillazine.org/Network.cookie.lifetimePolicy
 
Внимание: Cookie активно используются многими веб-ресурсами в процессе контроля и слежки за пользовательской активностью. Похищение и анализ cookie является потенциально опасной и серьезной атакой, приводящей к глобальным утечкам пользовательских данных и их несанкционированному использованию.


- USER AGENT

Строка User-Agent (часть HTTP-заголовка) используется для связи и передачи содержимого (контента) между клиентской программой и сервером. С помощью ее анализа сервер определяет оптимальные параметры для взаимодействия на основании уже имеющихся спецификаций того или иного программного обеспечения, данных о его назначении (браузер, почтовый клиент и т.п.) и текущей версии.

Создание пустого или поддельного значения useragent. Для запрета передачи каких-либо данных об UA, создайте новую текстовую строку с пустым значением (нажатием ПКМ в любом месте окна настроек):

    general.useragent.override=[пустое значение]

или, чтобы замаскировать свой UA и ОС под чужие (к примеру, работая в Linux):

    general.useragent.override="Mozilla/5.0 (Windows NT 6.1; rv:38.0) Gecko/20100101 Firefox/38.0"

Во втором случае вы можете внести в настройки браузера добавочные поддельные строки и их расширенные значения, например:

    general.useragent.override", "Mozilla/5.0 (Windows NT 6.1; rv:38.0) Gecko/20100101 Firefox/38.0"
    general.appname.override", "Netscape"
    general.appversion.override", "5.0 (Windows)"
    general.oscpu.override", "Windows NT 6.1"
    general.platform.override", "Win32"
    general.productSub.override", "20100101"
    general.buildID.override", "20100101"
    browser.startup.homepage_override.buildID", "20100101"

однако это может оказаться излишним.

https://developer.mozilla.org/en-US/docs/Web/HTTP/Gecko_user_agent_string_reference

Примечание: Вы можете найти поддельные значения UA здесь: http://www.useragentstring.com/pages/useragentstring.php. Пожалуйста, выбирайте наиболее общеупотребимые варианты (как это показано в примере выше), стараясь "не выделяться" из общей массы браузеров.

Внимание: Для предотвращения утечек информации об используемой ОС и браузере посредством анализа UA, дополнительно запретите JavaScript глобально!


- LOCALE, LANGUAGES

Маскировка локали браузера - с национальной (ru) под английскую:

    general.useragent.locale=en

http://kb.mozillazine.org/General.useragent.locale

Игнорирование национальной (текущей) локали операционной системы и использование значения из general.useragent.locale:

    intl.locale.matchOS=false

http://kb.mozillazine.org/Intl.locale.matchOS

Сброс (маскировка) предпочитаемых языков до en-us/en:

    intl.accept_languages=en-us,en

Отключение автопроверки орфографии:

    layout.spellcheckDefault=0

http://kb.mozillazine.org/Layout.spellcheckDefault

Внимание: Рекомендуется ставить нелокализованную (английскую, en-us) версию Firefox или отключить/удалить дополнение с локализацией!


- REFERERS

Referer - заголовок в протоколе HTTP, содержащий URI источника запроса. Анализируя referer, сервер может определить, откуда (с какого предыдущего веб-ресурса) исходит запрос. Когда пользователь нажимает на ссылку, браузер шлет запрос серверу-владельцу конечной веб-страницы; такой запрос включает referer, который уведомляет, с какой страницы пользователь собирается перейти на целевой ресурс.

Глобальный запрет отсылки рефереров:

    network.http.sendRefererHeader=0 (рекомендовано)

Более щадящий режим: отсылка рефереров только при нажатии на ссылку, но не на графику и т.п.:

    network.http.sendRefererHeader=1 (не рекомендовано)

http://kb.mozillazine.org/Network.http.sendRefererHeader

Запрет отсылок рефереров с одного (HTTPS) на другой HTTPS-сайт: 

    network.http.sendSecureXSiteReferrer=false (настройка может отсутствовать или использоваться в Android)

http://kb.mozillazine.org/Network.http.sendSecureXSiteReferrer


- REDIRECTIONS

Блокирование автоматических перенаправлений на другую страницу и предупреждение пользователя о таких попытках (с выбором решения); определение лимита перенаправлений:
 
    network.http.prompt-temp-redirect=true
    network.http.redirection-limit=1

https://support.mozilla.org/en-US/questions/1025367


- AUTOREFRESH

Запрет автообновления страницы:

    accessibility.blockautorefresh=true

https://support.mozilla.org/en-US/questions/1025367


- POPUPS

Блокирование всплывающих окон и показ предупреждения об их блокировании:

    dom.disable_open_during_load=true
    browser.popups.showPopupBlocker=true

http://kb.mozillazine.org/Pop-ups_not_blocked

https://support.mozilla.org/en-US/questions/675692

Блокирование всплывающих окон, инициируемых сторонними плагинами Flash или Java: 

    privacy.popups.disable_from_plugins=2

http://kb.mozillazine.org/Privacy.popups.disable_from_plugins


- IMAGES, FAVICONS

Запрет загрузки всех изображений. Это наиболее полный способ блокирования и запрета загрузки контента:

    permissions.default.image=2 (рекомендовано)

Более щадящая настройка позволяет загружать изображения только с посещаемого сервера и блокировать изображения, подгружаемые со сторонних (third-party) серверов:

    permissions.default.image=3 (не рекомендовано)

http://kb.mozillazine.org/Permissions.default.image

Запрет проигрывания анимации графики (*.gif и прочие):

    image.animation_mode=none

http://kb.mozillazine.org/Firefox_:_Tips_:_Animated_Images

Запрет отображения и хранения фавиконов (иконок сайта):

    browser.chrome.site_icons=false
    browser.chrome.favicons=false

http://kb.mozillazine.org/Browser.chrome.site_icons

http://kb.mozillazine.org/Browser.chrome.favicons


- PASSWORDS, FORMS

Запрет хранения логинов и паролей к сайтам:

    signon.rememberSignons=false
    signon.storeWhenAutocompleteOff=false

https://support.mozilla.org/en-US/questions/889884

Запрет на автоматический ввод связок логин/пароль в формы на страницах:

    signon.autofillForms=false

http://kb.mozillazine.org/Signon.autofillForms

Отключение синхронизации паролей посредством Firefox Sync:

    services.sync.prefs.sync.signon.rememberSignons=false

Отключение автозаполнения веб-форм: установка запрета на хранение поисковых запросов и прочих данных, введенных ранее в текстовые веб-формы. Когда вы вводите данные в формы веб-страниц (например, в поисковой строке), при следующем визите Firefox подставит сохраненное значение. Чтобы запретить хранение и подстановку данных, установите:

    browser.formfill.enable=false
    browser.formfill.expire_days=0
    browser.formfill.saveHttpsForms=false

https://support.mozilla.org/en-US/questions/813403

Отключение синхронизации автозаполнения форм посредством Firefox Sync

    services.sync.prefs.sync.browser.formfill.enable=false


- NETWORK: PIPELINING, DNS, PREFETCH, PING, PORTS, SSl

Pipelining - включение и определение количества параллельных запросов (в том числе - при использовании прокси и защищенного SSL-соединения). Протокол HTTP позволяет осуществлять множественные параллельные запросы к сайту (не дожидаясь ответа от сервера). Этот процесс известен как pipelining. Он сокращает время загрузки контента, однако не все серверы в состоянии поддерживать его. Для активации pipelining (и запрета его по защищенным SSL-соединениям во избежание ошибок) установите:

    network.http.pipelining=true
    network.http.pipelining.ssl=false
    network.http.version=1.1 (не создавайте эту настройку, она присутствует по умолчанию)

http://kb.mozillazine.org/Network.http.pipelining

http://kb.mozillazine.org/Network.http.pipelining.ssl

http://kb.mozillazine.org/Network.http.version

Активация pipelining при использовании прокси-сервера:

    network.http.proxy.pipelining=true
    network.http.proxy.version=1.1  (не создавайте эту настройку, она присутствует по умолчанию)

http://kb.mozillazine.org/Network.http.proxy.keep-alive

http://kb.mozillazine.org/Network.http.proxy.version

Для "удержания" (keep-alive) процесса pipelining проверьте следующую опцию:

    network.http.keep-alive=true

http://kb.mozillazine.org/Network.http.keep-alive

Установка предельного количества запросов pipelining:

    network.http.pipelining.maxrequests=32 (по умолчанию; увеличивать значение не рекомендуется)

http://kb.mozillazine.org/Network.http.pipelining.maxrequests

Запрет prefetching - предварительного запроса DNS для всех ссылок на активной странице (с целью ускорения последующей загрузки). Эта функция позволяет браузеру в фоновом режиме определять DNS для различного веб-контента (ссылок, графики, CSS, JavaScript и т.п.). Ее необходимо отключить:

    network.dns.disablePrefetch=true

http://kb.mozillazine.org/Network.dns.disablePrefetch

Запрет предварительного запроса DNS для всех ссылок на активной HTTPS-защищенной странице:

network.dns.disablePrefetchFromHTTPS=true (настройка может отсутствовать или устареть)

Запрет предварительной загрузки страницы, которую Firefox считает логически последующей:

    network.prefetch-next=false

http://kb.mozillazine.org/Network.prefetch-next

Отправка DNS-запросов через удаленный прокси (при использовании TOR, прокси-сервера и т.п.) для предотвращения их утечки к провайдеру:

    network.proxy.socks_remote_dns=true

http://kb.mozillazine.org/Network.proxy.socks_remote_dns

Отключение DNS-запросов посредством IPv6:

    network.dns.disableIPv6=true

Запрет отправки уведомлений о нажатии на ссылку адресам, указанным в тэге "a" (атрибут "ping"). HTML5 позволяет использовать новый атрибут для элемента <a> под названием ping. Эта функция использует отсылает данные по URI, определенному в гиперссылке, если на нее нажимает пользователь. Это позволяет отслеживать активность и предпочтения пользователей и собирать статистику о них:

    browser.send_pings=false
    browser.send_pings.require_same_host=false

http://kb.mozillazine.org/Browser.send_pings

Запрет на определение и отправку параметров (типа) сетевого соединения (Wi-Fi, LAN и т.п.), текущей скорости:

    dom.netinfo.enabled=false

https://developer.mozilla.org/en-US/docs/Web/API/Navigator/connection

Запрет отправки beacon - специфических HTTP-данных, утекающих от юзерагента на сервер, особенно при покидании страницы:

    beacon.enabled=false

https://en.wikipedia.org/wiki/Web_beacon

Отключение гипотетически уязвимых алгоритмов MD5, RC4 и DES, используемых для защищенных соединений с серверами по SSL3:

    security.ssl3.ecdhe_ecdsa_rc4_128_sha=false
    security.ssl3.ecdhe_rsa_rc4_128_sha=false
    security.ssl3.rsa_rc4_128_md5=false
    security.ssl3.rsa_rc4_128_sha=false
    security.ssl3.rsa_des_ede3_sha=false


- TOR, PROXY

Внимание: Не изменяйте эти настройки, если вы не понимаете, что делаете!

Для большей сохранности передаваемых данных браузер может быть сконфигурирован на использование прокси-сервера, в том числе - в связке с TOR.

Примечание: Рекомендуется использовать TOR в связке с кэширующим прокси-сервером Polipo. Это простейший способ подключения к сети TOR. Некоторые настройки конфигурации Polipo также помогут усилить степень анонимности пользователя.

Включение и выключение соединения с TOR через прокси-сервер (ручная настройка):

    network.proxy.type=1 (ВКЛ, ручная настройка конфгурации - рекомендовано совместно с TOR и Polipo)

или:

    network.proxy.type=0 (ВЫКЛ, прямое соединение с интернетом)

http://kb.mozillazine.org/Network.proxy.type

Настройка адресов и портов HTTP, SSL, FTP-соединений через прокси в режиме "network.proxy.type=1" (например, при использовании Polipo и TOR):
 
HTTP:
    network.proxy.http=localhost
    network.proxy.http_port=8118
SSL:
    network.proxy.ssl=localhost
    network.proxy.ssl_port=8118
FTP:
    network.proxy.ftp=localhost
    network.proxy.ftp_port=8118

https://developer.mozilla.org/en-US/docs/Mozilla/Preferences/Mozilla_networking_preferences

Запрет прямого получения DNS от провайдера при использовании TOR + Polipo:

    network.proxy.socks_remote_dns=true

Соксификация:

    network.proxy.socks_version=5 (не создавайте эту настройку, она присутствует по умолчанию)
    network.proxy.socks=localhost
    network.proxy.socks_port=9050

http://kb.mozillazine.org/Network.proxy.socks_version

http://kb.mozillazine.org/Network.proxy.socks_port

Запрет использования прокси для некоторых локальных адресов. Множество сетей лимитируют доступ к публичным ресурсам через прокси-сервер. Эта опция сконфигурирована как "black-list", определяющий запреты на выход через прокси:

    network.proxy.no_proxies_on=localhost, 127.0.0.1

http://kb.mozillazine.org/Network.proxy.no_proxies_on

Запрет на установку соединений по определенным портам. Многие порты зарезервированы за разными службами, обслуживающими, к примеру, FTP, POP и т.п. Для предотвращения потенциального риска необходимо запретить обращения к ним (TOR - добавить порты 9050, 9051, 9150, 9151; I2P - порт 4444, Polipo - 8118):

    network.security.ports.banned=9050,9051,9150,9151,8118,4444

http://kb.mozillazine.org/Network.security.ports.banned


- MULTIMEDIA

Для отключения сбора HTML-видеостатистики установите:

    media.video_stats.enabled=false

https://developer.mozilla.org/en-US/docs/Web/API/HTMLVideoElement#Gecko-specific_properties

Выключение WebGL (рекомендовано при торможениях, сбоях и проблемах с видеокартой):

    webgl.disable-extensions=true
    webgl.disabled=true
    webgl.force-enabled=false
    webgl.min_capability_mode=true

Запрет OffscreenCanvas. Этот механизм обеспечивает возможность выполнения отрисовки через WebGL в отдельном потоке. Запуск WebGL в отдельном потоке производится с помощью API OffscreenCanvas, добавленного в систему Workers, предоставляющую средства для фонового выполнения длительных JavaScript-операций (даже при уже закрытом приложении!) Для отключения установите:

    gfx.offscreencanvas.enabled=false (FF 44 и выше)

https://developer.mozilla.org/en-US/docs/Web/API/OffscreenCanvas

Запуск мультимедийного содержимого страницы (при помощи плагинов) только с явного согласия пользователя (по нажатию ЛКМ на видео-/аудиоклипе):

    plugins.click_to_play=true

Запрет автопроигрывания мультимедийного содержимого:

    media.autoplay.enabled=false
    media.audio_data.enabled=false (настройка может отсутствовать или устареть)

Отключение медиакодеков:

    media.ogg.enabled=false
    media.opus.enabled=false
    media.raw.enabled=false
    media.wave.enabled=false
    media.webm.enabled=false
    media.webvtt.enabled=false
    media.gmp-gmpopenh264.provider.enabled=false
    media.webaudio.enabled=false (настройка может отсутствовать или устареть)

https://support.mozilla.org/en-US/questions/992868

Web Speech - отключение распознавания (Text-to-Speech) и синтезирования речи (Asynchronous Speech Recognition):

    media.webspeech.recognition.enable=false
    media.webspeech.synth.enabled=false

https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API


- PLUGINS (FLASH, JAVA)

Настройка (блокирование) подключенных плагинов. Плагин - стороннее программное обеспечение, которое позволяет браузеру обрабатывать веб-контент, который он не может воспроизвести самостоятельно. Обычно это проприетарные (несвободные) патентованные форматы для обработки аудио- и видео-содержимого (Adobe Flash, Apple QuickTime, Microsoft Silverlight), а также онлайн-игры, презентации, средства для перехвата закачек и передачи их в специальные программы-даунлоадеры - uTorrent, Free Download manager и т.п.

Рекомендовано полное глобальное отключение:

    plugin.default.state=0

https://support.mozilla.org/en-US/questions/1002509

Отключение отдельных плагинов:

    plugin.state.flash=0 
    plugin.state.java=0
    plugin.state.quicktime=0

Допустимые значения:

    plugin.state.название_плагина=0 (никогда не активировать);
    plugin.state.название_плагина=1 (спрашивать перед активацией);
    plugin.state.название_плагина=2 (всегда автоактивировать)

Запрет запуска Plugin-container. Каждый сторонний плагин запускается в независимом процессе и позволяет браузеру продолжить свою работу, даже если произошел сбой плагина. Plugin-container требует большого количества оперативной памяти (RAM).

    dom.ipc.plugins.enabled=false (возможно, может не работать в новых версиях браузера)

https://support.mozilla.org/en-US/kb/what-is-plugin-container

Отключение телеметрических сообщений о крахе plugin-container, обеспечивающего работу флэш-плейера:

    dom.ipc.plugins.flash.subprocess.crashreporter.enabled=false
    dom.ipc.plugins.reportCrashURL=false

https://support.mozilla.org/en-US/kb/send-plugin-crash-reports-help-improve-firefox

Отключение запроса "Вы хотите установить Flash-плагин, необходимый для отображения этой страницы?" и подобных:

    plugins.hideMissingPluginsNotification=true
    plugins.notifyMissingFlash=false

https://support.mozilla.org/en-US/questions/969127


- SESSIONS, HISTORY

Session Restore - полное отключение механизма хранения сессий, включая посещенные (закрытые и открытые) ссылки, данные форм, cookies, POST-data и т.п.:

    browser.sessionstore.enabled=false

http://kb.mozillazine.org/Browser.sessionstore.enabled

Отключение механизма хранения данных сессии: никакие данные не будут сохранены при внезапном сбое браузера:

    browser.sessionstore.privacy_level=2

http://kb.mozillazine.org/Browser.sessionstore.privacy_level

Отключение механизма хранения данных сессии: никакие данные не будут сохранены при штатном выходе из браузера (не связанном с внезапным сбоем, перезагрузкой при установке дополнений):

    browser.sessionstore.privacy_level_deferred=2

http://kb.mozillazine.org/Browser.sessionstore.privacy_level

Ограничение на хранение количества и сведений о недавно закрытых вкладках и возможности их нового открытия в пределах одной сессии:

    browser.sessionstore.max_tabs_undo=0

http://kb.mozillazine.org/Browser.sessionstore.max_tabs_undo

Ограничение на хранение количества и сведений о недавно закрытых окнах в пределах одной сессии:

    browser.sessionstore.max_windows_undo=0

http://kb.mozillazine.org/Browser.sessionstore.max_windows_undo

Отмена автоматического хранения сведений об активной сессии и возможности ее восстановления в случае перезагрузки в связи с обновлением дополнений и т.п.:

    browser.sessionstore.resume_session_once=false

http://kb.mozillazine.org/Browser.sessionstore.resume_session_once

Запрет попытки восстановления активной сессии в случае краха браузера:

    browser.sessionstore.resume_from_crash=false

http://kb.mozillazine.org/Browser.sessionstore.resume_from_crash

Ограничения количества шагов при возврате на посещенные страницы (команда "Назад"):

    browser.sessionhistory.max_entries=5

Примечание: Если вы измените значение на "0", то не сможете воспользоваться кнопкой "Назад".

https://wiki.mozilla.org/Firefox/session_restore

Определение количества недавно посещенных страниц, которые станут хранится в памяти и не будут рендериться заново. Улучшает работу команд "Назад" и "Вперед". Эта опция отличается от сходной опцией, связанной кэшированием в оперативной памяти (RAM). Значение "-1" ("минус один") автоматически определяет количество страниц и зависит от общего размера RAM: 

    browser.sessionhistory.max_total_viewers=-1 (по умолчанию; рекомендовано)

http://kb.mozillazine.org/Browser.sessionhistory.max_total_viewers

Ограничение количества крахов браузера, после которых будет показана страница "about:sessionrestore":

    browser.sessionstore.max_resumed_crashes=0

http://kb.mozillazine.org/Browser.sessionstore.max_resumed_crashes

https://wiki.mozilla.org/Firefox/session_restore

Places (система хранения закладок, истории, другой пользовательской информации) - отмена хранения истории посещений и загрузок:

    places.history.enabled=false

https://wiki.mozilla.org/Places

Отмена подменю с ранее посещенными сайтами, выпадающего под адресной строкой в момент ручного набора веб-адреса:

    browser.urlbar.maxRichResults=0

http://kb.mozillazine.org/Browser.urlbar.maxRichResults

Запрет на подстановку/автодополнение данных из истории (history) и закладок (bookmarks):

    browser.urlbar.autocomplete.enabled=false

http://kb.mozillazine.org/Changing_autocomplete_behavior_-_Firefox

Внимание: хранение информации о сессиях, недавно открытых вкладках, посещенных сайтах, загрузках и т.п., а также наличие возможности их восстановления могут выдать гипотетической атакующей стороне пользовательские предпочтения и прочую информацию. 

Сокращение количества резервных копий закладок браузера (bookmarks):

    browser.bookmarks.max_backups=1

http://kb.mozillazine.org/Browser.bookmarks.max_backups


- CACHE

Внимание: если вы настраиваете Firefox для Android или iOS, не изменяйте настройки, описываемые в данном разделе, особенно если на вашем устройстве нет достаточного (> 1 Гб) количества оперативной памяти (RAM)!

Запрет кэширования файлов на диск (в том числе - поступающих по защищенным соединениям):

    network.http.use-cache=false

http://kb.mozillazine.org/Network.http.use-cache

Запрет использования дискового кэша: 

    browser.cache.disk.enable=false

http://kb.mozillazine.org/Browser.cache.disk.enable

Запрет использования дискового кэша, если используется шифрованное SSL-соединение (и обрабатываются приватные пользовательские данные):
 
    browser.cache.disk_cache_ssl=false

http://kb.mozillazine.org/Browser.cache.disk_cache_ssl

Запрет создания кэша для просмотра страниц в офлайне:

    browser.cache.offline.enable=false

http://kb.mozillazine.org/Browser.cache.offline.enable

Запрет автоматического управления дисковым кэшем (если он включен):

    browser.cache.disk.smart_size.enabled=false

https://developer.mozilla.org/en-US/docs/Mozilla/Preferences/Mozilla_networking_preferences#Cache

Обнуление (запрет) объема дискового кэша, хранящегося на винчестере (в том числе - и офлайн-кэша):

    browser.cache.disk.capacity=0
    browser.cache.offline.capacity=0

http://kb.mozillazine.org/Browser.cache.disk.capacity

Примечание: включать в совокупности с browser.cache.disk.smart_size.enabled=false

Разрешение хранения кэша в оперативной памяти (в том числе и данных, полученных по шифрованным SSL-соединениям):

    browser.cache.memory.enable=true

http://kb.mozillazine.org/Browser.cache.memory.enable

Определение количества оперативной памяти, выделяемой под кэш (в зависимости от общего объема RAM):

    browser.cache.memory.capacity=-1 (автоматическое определение; рекомендуется)

Допустимые значения:

0 - оперативная память не используется (не рекомендуется; см. примечание ниже);

n (целое цифровое значение) - количество килобайт, выделенных на кэш.

Примечание: Требует browser.cache.memory.enable=true

http://kb.mozillazine.org/Browser.cache.memory.capacity

Внимание: одновременный запрет на хранение кэша как в оперативной памяти, так и на винчестере, может привести к проблемам.


- GEO-IP

Отключение геолокации. Firefox располагает встроенными средствами передачи геоданных (вашего местонахождения). При этом используются сведения, получаемые от геолокационных средств операционной системы, сетей Wi-Fi, телефонных и интернет-операторов, а также реальный IP-адрес. Кроме того, вышеперечисленные данные отсылаются на серверы Google. Это серьезный источник утечек и слежения за пользователем; его следует отключить: 

    geo.enabled=false
    geo.wifi.uri=
    browser.geolocation.warning.infoURL=

https://www.mozilla.org/en-US/firefox/geolocation/


- SEARCH: GEO-IP

Поисковый механизм по умолчанию использует данные, связанные с геолокацией (вашим реальным местонахождением, определяемым по IP-адресу). Эти данные отсылаются на серверы Mozilla и Google. Кроме того, Google собирает и хранит данные о ваших поисковых запросах и предпочтениях. Это серьезный источник утечек и слежения за пользователем; его следует отключить.

Отключение автоподстановки при поиске (автоматической передачи текста, набираемого в окне поиска, на поисковый сайт - без явного подтверждения со стороны пользователя). Эту функцию рекомендовано заблокировать:

    browser.search.suggest.enabled=false

http://kb.mozillazine.org/Browser.search.suggest.enabled

Отключение геопозиционирования браузера (GeoIP) при работе с поисковыми серверами. Firefox располагает встроенными средствами передачи геоданных (вашего местонахождения). При этом используются сведения, получаемые от геолокационных средств операционной системы, сетей Wi-Fi, телефонных и интернет-операторов, а также реальный IP-адрес. Кроме того, вышеперечисленные данные отсылаются на серверы Google. Необходимо установить:

    browser.search.geoSpecificDefaults=false
    browser.search.geoip.url=false (настройка может отсутствовать или устареть)
    browser.search.countryCode=US (настройка может отсутствовать или устареть)
    browser.search.region=US (настройка может отсутствовать или устареть)

https://support.mozilla.org/en-US/kb/how-stop-firefox-making-automatic-connections


- UPDATES: BROWSER, PERSONAS, SEARCH PLUGINS

Отмена автоматического обновления браузера. Один раз в день Firefox отсылает на серверы Mozilla информацию о браузере, его версии, операционной системе и языковой локали и, в случае необходимости, пытается автоматически установить обновления браузера. Для отключения этой функции установите:

    app.update.auto=false

    app.feedback.baseURL=
    app.support.baseURL=
    app.update.url=
    app.update.url.details=
    app.update.url.manual=

Отмена автоматического обновления поисковых плагинов:

    browser.search.update=false

Personas - отключение обновления "легковесных тем" оформления браузера:

    lightweightThemes.update.enabled=false
    lightweightThemes.getMoreURL=
    lightweightThemes.recommendedThemes=

http://kb.mozillazine.org/Themes

Отключение появления автозагружаемой страницы "Что нового" после обновления браузера:

    browser.startup.homepage_override.mstone=ignore

http://kb.mozillazine.org/Browser.startup.homepage_override.mstone

Запрет проверки браузера, установленного по умолчанию в операционной системе:

    browser.shell.checkDefaultBrowser=false

http://kb.mozillazine.org/About:config_entries


- UPDATES: ADDONS

Отмена автоматического обновления дополнений. Firefox отсылает на серверы Mozilla информацию о браузере, его версии, операционной системе и языковой локали и, в случае необходимости, пытается автоматически установить обновления браузерных дополнений. Для отключения этой функции установите:

    extensions.update.autoUpdateDefault=false
    extensions.update.enabled=false
    extensions.update.url=

http://kb.mozillazine.org/About:config_entries#Extensions.

Отключение профилируемой информации о дополнениях и блокирование отсылки пользовательских метаданных об  использовании дополнений. Firefox, отталкиваясь от списка уже установленных дополнений, предлагает новые на странице "Get Add-ons" в менеджере дополнений. При этом Mozilla получает и анализирует информацию, поступающую от браузера: номер версии, IP-адрес и прочее. Это можно отключить, установив:

    extensions.getAddons.cache.enabled=false

https://blog.mozilla.org/addons/how-to-opt-out-of-add-on-metadata-updates/

Отключение поиска тем и дополнений. Firefox предлагает сторонние дополнения и темы, обращаясь к серверу Mozilla и передавая ему для анализа пользовательские запросы и метаданные. Установите:

    extensions.getAddons.search.url=

http://kb.mozillazine.org/Extensions.getAddons.search.url

Отключение предложения "предпочтительных дополнений". Firefox рекламирует сторонние дополнения и темы, обращаясь к серверу Mozilla и передавая ему для анализа пользовательские метаданные. Установите: 

    extensions.getAddons.recommended.url=
    extensions.getAddons.getWithPerformance.url=
    extensions.webservice.discoverURL=

http://kb.mozillazine.org/Extensions.getAddons.recommended.url

Отключение закачки базы нежелательных дополнений с сервера Mozilla. Firefox соединяется с сервером Mozilla и скачивает "черный список" вредоносных и подозрительных сторонних дополнений. Это функционал блокируется следующими настройками:

    extensions.blocklist.enabled=false
    extensions.blocklist.itemURL=
    extensions.blocklist.url=
    extensions.blocklist.detailsURL=

http://kb.mozillazine.org/Extensions.blocklist.enabled

Внимание: в рекомендуемой конфигурации Firefox в принципе вообще нежелательно устанавливать какие-то дополнения. В крайнем случае - используйте только хорошо известные расширения, скачивая их из проверенных источников; оптимальный вариант -  выпускаемые исключительно под свободным лицензиями; см. список: 

https://www.gnu.org/software/gnuzilla/addons.html

Внимание: Помните, что внутренние установки дополнений могут войти в конфликт с настройками, рассматриваемыми в данном руководстве, или перезаписать их!


- CLEAN

Очистка истории, сессий, паролей, кэша, cookies и т.п. при выходе из браузера:

    privacy.sanitize.sanitizeOnShutdown=true

(дополнительные настройки очистки):

    privacy.clearOnShutdown.cache=true
    privacy.clearOnShutdown.cookies=true
    privacy.clearOnShutdown.downloads=true
    privacy.clearOnShutdown.formdata=true
    privacy.clearOnShutdown.history=true
    privacy.clearOnShutdown.offlineApps=true
    privacy.clearOnShutdown.passwords=true
    privacy.clearOnShutdown.sessions=true
    privacy.clearOnShutdown.siteSettings=true
    privacy.clearOnShutdown.sessions=true

http://kb.mozillazine.org/About:config_entries


- DOWNLOADS/OPEN

Отключение проверки файлов для предотвращения блокирования "подозрительных" закачек. Данная опция позволяет пользователям Windows автоматически проверять файлы антивирусом после их скачивания. Программы, обеспечивающие безопасности (антивирусы, многие файерволлы и прочие комплексные решения), могут запрещать закачку некоторых файлов, к примеру - закачка исполнимых файлов в среде Windows (например *.exe или *.msi) может быть заблокирована. В подобных случаях необходимо отключить проверку, особенно если вы не желаете, чтобы скачиваемые вами файлы проверялись "в облаке" или о них передавалась бы какая-либо информация - это нарушает вашу приватность:

    browser.download.manager.scanWhenDone=false

http://kb.mozillazine.org/Browser.download.manager.scanWhenDone

https://support.mozilla.org/en-US/kb/cant-download-or-save-files

Отключение добавления списка закачанных файлов в список "Последние документы":

    browser.download.manager.addToRecentDocs=false

https://developer.mozilla.org/en-US/docs/Download_Manager_preferences

http://kb.mozillazine.org/Browser.download.manager.addToRecentDocs

Запрет на открытие небезопасных типов файлов при их загрузке (*.jar, *.zip, etc.)

Mozilla поддерживает jar: - протокол, который позволяет браузеру "напрямую" загружать файлы из jar-архивов. Их открытие/исполнение может привести к проблемам в безопасности. Установите:

    network.jar.open-unsafe-types=false

http://kb.mozillazine.org/Network.jar.open-unsafe-types


- SERVICES, TELEMETRY

- DNT, TRACKING PROTECTION

“Do Not Track” - механизм, который пытается сообщить сайтам о том, что пользователь браузера не желает, чтобы посещаемые им ресурсы отслеживали его активность, используя рекламные и аналитические сервисы. Учитывая агрессивность политики таких сервисов, “Do Not Track” - одна из самых бесполезных браузерных функций, поскольку подобная "просьба о неотслеживании" ни к чему не обязывает владельцев следящих сайтов. Необходимо установить:

    privacy.donottrackheader.enabled=false
    privacy.donottrackheader.value=1

http://kb.mozillazine.org/Privacy.donottrackheader.enabled

http://kb.mozillazine.org/Privacy.donottrackheader.value

https://support.mozilla.org/en-US/kb/how-do-i-turn-do-not-track-feature

Отключение загрузки списка следящих сайтов и механизма trackingprotection. Firefox скачивает с сайта Mozilla список "следящих" сайтов и пытается блокировать их, если пользователь работает в режиме "Private Browsing". Это увеличивает расходуемый трафик и гипотетически может раскрыть ваши пользовательские предпочтения, в частности - список посещаемых сайтов. Этот механизм тоже следует отключить (учитывая общую бесполезность сервиса “Do Not Track”):

    privacy.trackingprotection.enabled=false
    browser.trackingprotection.gethashURL=
    browser.trackingprotection.updateURL=

https://developer.mozilla.org/en-US/Firefox/Privacy/Tracking_Protection


- POCKET

Блокирование сервиса Pocket. Проприетарное приложение Pocket (ранее известное как Read It Later) позволяет сохранять ссылки на тексты в облачном хранилище для их дальнейшего прочтения, храня таким образом данные о пользовательской активности и синхронизируя их между всеми устройствами, подписанным на услуги сервиса. Это может деанонимизировать пользователей и раскрыть их предпочтения. Установите:

    browser.pocket.enabled=false

Примечание: К сожалению, данная настройка блокирует только кнопку сервиса; сам сервис не удаляется!


- GOOGLE

Блокирование защиты от фишинговых и зараженных сайтов - Google's SafeBrowsing (в целях предотвращения отсылки адресов посещаемых сайтов и пользовательских метаданных для анализа в Google):

Дважды в час Firefox скачивает базы данных Google, предназначенные для обеспечения блокирования зараженных, подозрительных или фишинговых/поддельных сайтов. Для проверки ресурсов/файлов, не присутствующих в базах, Firefox отсылает пользовательские данные в Google, включая ссылки и прочие метаданные. Это может деанонимизировать пользователей и раскрыть их предпочтения. Это серьезный источник утечек и слежения за пользователем; его следует отключить:

    browser.safebrowsing.enabled=false
    browser.safebrowsing.malware.enabled=false
    browser.safebrowsing.downloads.enabled=false
    browser.safebrowsing.downloads.remote.enabled=false
    services.sync.prefs.sync.browser.safebrowsing.enabled=false
    services.sync.prefs.sync.browser.safebrowsing.malware.enabled=false

    browser.safebrowsing.appRepURL=
    browser.safebrowsing.gethashURL=
    browser.safebrowsing.malware.reportURL=
    browser.safebrowsing.reportErrorURL=
    browser.safebrowsing.reportGenericURL=
    browser.safebrowsing.reportMalwareErrorURL=
    browser.safebrowsing.reportMalwareURL=
    browser.safebrowsing.reportPhishURL=
    browser.safebrowsing.reportURL=
    browser.safebrowsing.updateURL=

http://kb.mozillazine.org/Browser.safebrowsing.enabled

http://kb.mozillazine.org/Browser.safebrowsing.malware.enabled


- SYNC

Блокирование Firefox Sync - удаленной синхронизации пользовательских данных. Sync - набор компонентов, который при помощи единого пользовательского аккаунта удаленно синхронизирует данные на разных устройствах с установленным Firefox  (закладки, историю, пароли, данные форм, открытые вкладки и т.п.). 

Внимание: Непредвиденная утечка подобных данных (логинов, паролей, cookie) в процессе синхронизации, передачи их за пределы отдельного устройства или во время хранения - невероятно критична и опасна! 

Чтобы отключить сервис, установите: 

    services.sync.serverURL=
    services.sync.tokenServerURI=
    services.push.serverURL=
    services.sync.fxa.privacyURL=
    services.sync.fxa.termsURL=
    services.sync.jpake.serverURL=
    services.sync.privacyURL=
    services.sync.statusURL=
    services.sync.syncKeyHelpURL=
    services.sync.termsURL=

    identity.fxaccounts.auth.uri=
    identity.fxaccounts.remote.force_auth.uri=
    identity.fxaccounts.remote.signin.uri=
    identity.fxaccounts.remote.signup.uri=
    identity.fxaccounts.settings.uri=

    services.sync.engine.addons=false
    services.sync.engine.bookmarks=false
    services.sync.engine.history=false
    services.sync.engine.passwords=false
    services.sync.engine.prefs=false
    services.sync.engine.tabs=false

https://wiki.mozilla.org/Services/Sync/Addon_Sync


- MARKETPLACE

Блокирование Firefox Discover Apps (Firefox Marketplace):

    browser.apps.URL=

https://support.mozilla.org/en-US/questions/1064312


- PDF

Запрет просмотра PDF-документов средствами браузера (средствами HTML5):

    pdfjs.disabled=true

https://support.mozilla.org/en-US/questions/943119


- FONTS

Отключение загрузки сторонних шрифтов. Существуют разные модели угроз и атак посредством поврежденных сторонних шрифтов, закачиваемых в браузер при просмотре сайтов, которые их используют. Установите:

    gfx.downloadable_fonts.enabled=false
    gfx.downloadable_fonts.woff2.enabled=false
    gfx.font_rendering.opentype_svg.enabled=false

https://wiki.mozilla.org/Firefox3.1/Downloadable_Fonts_Security_Review


- TILES

Запрет рекламных предложений, размещаемых Mozilla в Tiles ("плитках"). Tiles - технология создания визуализируемого списка посещаемых сайтов и ротации рекламы, размещаемых в новых табах. Firefox шлет в Mozilla информацию о количестве нажатий (кликов) на определенную ссылку, IP-адрес пользователя и пересылает обратно рекламные предложения, внедряемые в браузер. Телеметрические функции могут собирать также информацию о наиболее часто посещаемых сайтах и данные геолокации. Список рекламных предложений периодически закачивается с сервера Mozilla и основывается на анализе пользовательских предпочтений. Это серьезный источник утечек и слежения за пользователем; его следует отключить: 

    browser.newtabpage.directory.ping=
    browser.newtabpage.directory.source=

https://support.mozilla.org/en-US/questions/1074600

Запрет принудительного создания/сохранения на винчестере скриншотов посещенных страниц (thumbnails), показываемых в новом табе ("часто посещаемые сайты"; технология Tiles). 

Вы должны самостоятельно(!) создать две новые строки (нажатием ПКМ в любом месте окна настроек): "Создать" - "Логическое":

    browser.pagethumbnails.capturing_disabled=true
    pageThumbs.enabled=false

https://developer.mozilla.org/en-US/docs/Mozilla/Preferences/Preference_reference/browser.pagethumbnails.capturing_disabled

https://support.mozilla.org/en-US/questions/973320


- SNIPPETS

Отключение отсылки статистической информации, связанной с технологией Snippets (англ.: "обрывок", "фрагмент", "ничтожество"). Домашняя страница Firefox, установленная по умолчанию (about:home), содержит встроенный механизм показа некоторой информации и одновременного слежения за пользовательскими предпочтениями. Раз в день Firefox соединяется с сервером Mozilla и затем предлагает новый "обрывок". Mozilla отслеживает количество нажатий на snippets, их имена, локаль браузера и его версию. Эта информация хранится на сервере Mozilla 60 дней. Для показа наиболее подходящих "обрывков", Firefox ежемесячно посылает на сервер Mozilla запрос о вашем местонахождении и IP-адресе. Некоторые "обрывки" интерактивны и могут распространять ваш почтовый адрес и телефонный номер, что особенно опасно. Это серьезный источник утечек и слежения за пользователем; его следует отключить: 

    browser.aboutHomeSnippets.updateUrl=
    browser.snippets.countryCode=US (в версии для Android)

https://wiki.mozilla.org/Firefox/Projects/Firefox_Start/Snippet_Service


- WebRTC

Блокирование WebRTC. WebRTC (Web Real-Time Communication) - специальная "черновая" спецификация API, который обеспечивает голосовое общение, видеочаты, обмен файлами по технологии P2P между браузерными приложениям без использования сторонних дополнений. Чтобы отключить его функционал, установите:

    media.peerconnection.enabled=false
    media.peerconnection.identity.enabled=false
    media.peerconnection.video.enabled=false
    media.websocket.enabled=false (настройка может отсутствовать)

http://kb.mozillazine.org/About:config


- HELLO

Блокирование Firefox Hello (службы текстового общения, аудио-и видеозвонков):

    loop.enabled=false
    loop.throttled2=false
    loop.feedback.baseUrl=
    loop.gettingStarted.url=
    loop.learnMoreUrl=
    loop.legal.ToS_url=
    loop.legal.privacy_url=
    loop.oauth.google.redirect_uri=
    loop.oauth.google.scope=
    loop.server=
    loop.soft_start_hostname=
    loop.support_url=
    loop.rooms.enabled=false

https://support.mozilla.org/en-US/kb/firefox-hello-video-and-voice-conversations-online

https://support.mozilla.org/en-US/questions/1043588


- SPDY

Блокирование SPDY. SPDY протокол, разработанный с участием Google для транспортировки веб-контента. SPDY видоизменяет веб-трафик с целью сокращения времени его загрузки путем компрессии, мультиплекса и механизма расстановки приоритетов. Чтобы отключить его, измените: 

    network.http.spdy.allow-push=false
    network.http.spdy.enabled=false
    network.http.spdy.enabled.http2=false
    network.http.spdy.enabled.http2draft=false
    network.http.spdy.enabled.v3=false
    network.http.spdy.enabled.v3-1=false
    media.http.spdy.enabled=false
    network.http.spdy.enabled.deps=false (может отсутствовать)

https://en.wikipedia.org/wiki/SPDY


- TELEMETRY

Блокирование отсылки телеметрии на серверы Mozilla. Эта функция шлет на серверы Mozilla данные об использовании, производительности браузера, особенностях пользовательского интерфейса, памяти и конфигурации оборудования, а также реальный IP. Кроме того, может собираться информация о посещаемых сайтах. Это серьезный источник утечек и слежения за пользователем; его следует отключить: 

    toolkit.telemetry.server=
    toolkit.telemetry.enabled=false
    toolkit.identity.enabled=false
    toolkit.crashreporter.infoURL=
    toolkit.telemetry.infoURL=

https://wiki.mozilla.org/Telemetry/faq


- TELEMETRY: EXPERIMENTS

Блокирование Telemetry Experiments. Experiments позволяет Firefox автоматически загружать и запускать некоторые дополнения. Установите:

    app.update.lastUpdateTime.experiments-update-timer=0
    experiments.enabled=false
    experiments.manifest.fetchIntervalSeconds=0
    experiments.manifest.uri=
    experiments.supported=false
    network.allow-experiments=false
    experiments.logging.dump=false (настройка может отсутствовать)

https://wiki.mozilla.org/Telemetry/Experiments


- HEALTH REPORT (FHR)

Отключение Health Report. Данная функция собирает расширенную информацию о работоспособности браузера и отсылает ее на серверы Mozilla, в частности: количество падений, сведения о медленной загрузке. Она включает в себя данные об оборудовании, операционной системе, версии браузера, установленных дополнениях (количество и тип), внутрибраузерных событиях, рендеринге, восстановлении сессий, их длительности, возрасте профиля, количестве посещенных страниц. Это серьезный источник утечек и слежения за пользователем; его следует отключить:

    datareporting.healthreport.service.firstRun=false
    datareporting.healthreport.service.enabled=false
    datareporting.healthreport.uploadEnabled=false
    datareporting.policy.dataSubmissionEnabled=false
    datareporting.healthreport.logging.dumpEnabled=false
    datareporting.healthreport.infoURL=
    datareporting.healthreport.documentServerURI=
    datareporting.healthreport.about.reportUrl=

https://support.mozilla.org/en-US/questions/1078303


- CRASH REPORTING

Отключение сrash reporting - отсылки отчета о сбоях. Эта функция отсылает на сервер Mozilla сведения о сбоях и падениях браузера, включая техническую информацию (состояние памяти и т.п.), время происшествия и посещаемые веб-ссылки, а также некоторую пользовательскую информацию. Необходимо блокировать адрес отсылки отчета:

    breakpad.reportURL=


- HEARTBEAT

Блокирование  Firefox Heartbeat - системы отсылки данных в Mozilla о пользовательских предпочтениях при использовании браузера и оценки его работы. Этот процесс называется "пульсом". Для отключения установите:

    browser.selfsupport.url= (возможно, настройка может существует только в версии для Android)

https://wiki.mozilla.org/Advocacy/heartbeat


- PREDICTOR (ex-SEER)

Блокирование механизма "network predictor" (бывший "seer"). Network predictor создает простейшие соединения с сервером, действуя подобно функции "hovers", когда курсор находится над определенной ссылкой. Firefox пытается предугадать дальнейшие действия пользователя на странице с целью увеличения производительность и скорости обработки контента на странице. Для отключения установите:

    network.seer.enabled=false (настройка может отсутствовать или устареть)

Ограничение (обнуление) размеры базы данных seer:

    network.seer.max-db-size=0 (настройка может отсутствовать или устареть)

Блокирование predictor (видоизмененного механизма seer):

    network.predictor.enabled=false
    network.predictor.enable-hover-on-ssl=false
    network.predictor.max-db-size=0

Отключение предварительных (гипотетических, "спекулятивных") соединений с сайтами. Для уменьшения времени загрузки Firefox открывает предварительные соединения с сайтами, когда пользователь наводит курсор на сохраненный скриншот сайта (см. сервис Tiles) на открытой новой вкладке, начинает искать в поле поиска или в поисковом поле новой вкладки (about:home). Для отключения установите:

    network.http.speculative-parallel-limit=0

https://support.mozilla.org/en-US/kb/how-stop-firefox-making-automatic-connections#w_speculative-pre-connections


- SHARE/SOCIALS

Блокирование Firefox Share. Архитектура Social API позволяет интегрировать браузер с соцсетями. При этом доступен следующий функционал:

а) интегрирование оповещений соцсетей на панели браузера.

б) интегрирование новостных лент, тикетов, списков друзей.

в) интегрирование голосовых, текстовых и видеочатов в доки или всплывающие окна.

г) интегрирование сервисов, связанных с распространением (рекомендацией, оценкой) веб-контента.

Для отключения установите:

    social.shareDirectory=
    social.directories=
    social.whitelist=
    social.remote-install.enabled=false
    social.share.activationPanelEnabled=false
    social.toast-notifications.enabled=false

https://wiki.mozilla.org/Firefox_Social_Integration


- CAST/CAPTURE/SCREENSHARING

Блокирование дополнительного функционала WebRTC WG (захват и видеотрансляция рабочих столов) и Media Capture Task Force:

    media.getusermedia.browser.enabled=false
    media.getusermedia.screensharing.enabled=false
    media.getusermedia.screensharing.allowed_domains=

https://wiki.mozilla.org/Media/getUserMedia

https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia

Отключение "Send Video To Device" (передача HTML5-видео в Roku, Chromecast и т.п.):

    browser.casting.enabled=false (настройка может присутствовать только в Android)

https://support.mozilla.org/en-US/kb/how-stop-firefox-making-automatic-connections


- DRM (Encrypted Media Extensions, EME)

Блокирование функций DRM ("Защищенный [платный] медиаконтент", EME). EME - проприетарный (closed-source) JavaScript API для воспроизведения защищенного видеоконтента в HTML. Content Decryption Module (CDM) предназначен для расшифрования, декодирования и демонстрации подобного видео. Это один из самых спорных  функционалов, включаемых в Firefox. Подобная технология называется "цифровыми наручниками". Для ее отключения измените:

    media.eme.enabled=false
    media.gmp-eme-adobe.enabled=false

https://wiki.mozilla.org/Media/EME


- WI-FI

Блокирование функционала, следящего за использованием WI-FI-сетей, а также разрешающего отладку браузера по WI-FI. Firefox собирает информацию о ближайших беспроводных точках доступа и вашем реальном IP-адресе и затем передает ее в ближайшему геолокационному провайдеру, а также в службу Google Location Services. Это раскрывает ваше местонахождение. Для отключения установите:

    network.tickle-wifi.enabled=false
    geo.wifi.uri=

    devtools.remote.wifi.scan=false
    devtools.remote.wifi.visible=false

http://kb.mozillazine.org/Geo.wifi.uri


- WORKERS

Запрет Web Workers - средства для фонового выполнения длительных JavaScript-операций. Данный сервис перехватывает сетевую активность средствами Service Workers. Обработчики сообщений, получаемых от сервера,  действуют, даже когда страница с web-приложением закрыта или неактивна, и не зависят от времени жизни приложения. Это сильно нагружает ресурсы системы и занимает большую часть оперативной памяти. Для отключения установите:

    dom.serviceWorkers.enabled=false
    dom.workers.enabled=false
    dom.workers.websocket.enabled=false

https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers


- HSTS

Запрет отслеживания с помощью технологии HSTS. Эта функция включена по умолчанию и не имеет встроенных настроек для ее блокирования. Механизм HSTS позволяет защищать соединения между сервером и браузером, принудительно активируя обращение к сайтам по протоколу HTTPS, и препятствует атакам, связанным с понижением уровня защиты (downgrade attack). Однако реализация HSTS аналогично внедрению в браузер т.н. supercookie ("неудаляемых cookie") и служит дополнительным средством отслеживания пользовательской активности. Firefox сохраняет данные HSTS в текстовом файле, расположенном в корне профиля браузера:

SiteSecurityServiceState.txt

    support.mozilla.org:HSTS	0	17849	1535470706051,1,0
    duckduckgo.com:HSTS		0	17849	1535470693691,1,0
    (...)

Это реальные "цифровые отпечатки" вашего браузера - серьезный источник утечек и слежения за пользователем; его следует отключить.

Для предотвращения отслеживания:

а) закройте Firefox;
б) откройте файл SiteSecurityServiceState.txt и удалите в нем все строки;
в) сохраните и закройте файл;
г) сделайте файл доступным только для чтения,

например (только в Linux):

    chmod 400 SiteSecurityServiceState.txt

д) проверьте права на файл. Они должны выглядеть следующим образом: 

    -r--------

https://en.wikipedia.org/wiki/HSTS

https://en.wikipedia.org/wiki/Downgrade_attack


- HARDWARE

Выключение аппаратного ускорения (рекомендовано при торможениях, сбоях и проблемах с видеокартой):

    layers.acceleration.disabled=true

https://support.mozilla.org/en-US/questions/1075336

Отключение сбора информации с сенсоров:

    device.sensors.enabled=false

https://wiki.mozilla.org/Sensor_API 

Отключение мониторинга аккумулятора:

    dom.battery.enabled=false

https://developer.mozilla.org/en-US/docs/Web/API/BatteryManager

Отключение взаимодействия с вибратором мобильного устройства:

    dom.vibrator.enabled=false

https://wiki.mozilla.org/B2G/QA/WebAPI_Test_Plan/Vibration

Отключение взаимодействия с микрофоном и веб-камерой:

    media.navigator.enabled=false
    media.navigator.video.enabled=false
    camera.control.autofocus_moving_callback.enabled=false
    camera.control.face_detection.enabled=false

https://wiki.mozilla.org/Media/getUserMedia


- INTERFACE

Отключение анимации элементов браузерного окна с целью увеличения "отзывчивости" интерфейса браузера:

    browser.fullscreen.animateUp=0
    browser.tabs.animate=false
    alerts.disableSlidingEffect=true
    nglayout.enable_drag_images=false

Отключение "улучшенной" новой страницы:

    browser.newtab.url=about:blank
    browser.newtabpage.enabled=false
    browser.newtabpage.enhanced=false
    browser.newtabpage.pinned=
    browser.startup.homepage=about:blank ("пустая страница"; рекомендуется)

Отмена плавной прокрутки (рекомендовано при торможениях, аппаратных сбоях и проблемах с видеокартой):

    general.smoothScroll=false

https://developer.mozilla.org/en-US/docs/Mozilla/Tech/XUL/Attribute/smoothscroll


## IV. ATENTION! ANDROID/iOS

Специальное предупреждение Mozilla о сборе, передаче, анализе и хранении пользовательских данных в специальной версии Firefox для мобильных систем. Будьте внимательны и осторожны!

**Firefox for Android and Firefox for iOS: In order to understand the performance of certain Mozilla marketing campaigns, Firefox sends data, including a Google advertising ID, IP address, timestamp, country, language/locale, operating system, app version, to our third party vendor. This data allows us to attribute an install to a specific advertising channel and optimize marketing campaign strategies.**

https://www.mozilla.org/en-US/privacy/firefox/
