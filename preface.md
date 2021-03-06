# Предисловие

OpenVPN - один из самых популярных в мире пакетов для настройки виртуальной частной сети (VPN). OpenVPN предоставляет расширяемую платформу VPN, которая была разработана для облегчения настройки конкретного сайта, например, предоставляя возможность распространять настроенный пакет установки клиентам или поддерживая альтернативные методы аутентификации через интерфейс модуля плагина OpenVPN. Он широко используется многими частными лицами и компаниями, а некоторые поставщики услуг даже предлагают OpenVPN доступ в качестве услуги для пользователей в удаленных, незащищенных средах.
В этой книге вы найдете множество различных рецептов для настройки, мониторинга и устранения неполадок сети OpenVPN. Опыт автора в устранении неполадок OpenVPN и сетевых конфигураций позволяет ему поделиться своими идеями и решениями, чтобы помочь вам получить максимальную отдачу от настройки OpenVPN.

## О чем рассказывает эта книга

Глава 1, _Сети Точка-точка_, дает введение в настройку OpenVPN. Рецепты основаны на сети типа "Точка-точка", что означает, что только один клиент может подключиться одновременно.

Глава 2, _Клиент-серверные IP-сети_, знакомит читателя с наиболее часто используемой моделью развертывания OpenVPN: один сервер с несколькими удаленными клиентами, способными маршрутизировать IP-трафик. Эта глава дает основу для многих рецептов, найденных в других главах.

В главе 3, _Сети типа клиент-сервер Ethernet_, рассматривается еще одна популярная модель развертывания OpenVPN: один сервер с несколькими клиентами, способный маршрутизировать трафик Ethernet. Это включает в себя не IP-трафик, а также мосты. Вы также узнаете об использовании внешнего DHCP-сервера и использовании файла состояния OpenVPN.

Глава 4, _PKI, сертификаты и OpenSSL_, знакомит вас с инфраструктурой открытых ключей (PKI) и сертификатами X. 509, которые используются в OpenVPN. Вы узнаете, как создавать, управлять, манипулировать и просматривать сертификаты, а также узнаете о взаимодействии между OpenVPN и библиотеками OpenSSL, от которых он зависит.

Глава 5, _Сценарии и плагины_, охватывает мощные возможности сценариев и плагинов, которые предлагает OpenVPN. Вы научитесь использовать клиентские сценарии, которые можно использовать для привязки процесса подключения к конкретным потребностям сайта. Вы также узнаете о серверных сценариях и использовании плагинов OpenVPN.

Глава 6, _Устранение неполадок OpenVPN-конфигураций_, посвящена устранению неполадок неправильных конфигураций OpenVPN. Некоторые из конфигурационных директив, используемых в этой главе, не были продемонстрированы ранее, поэтому даже если ваша настройка работает должным образом, эта глава все равно будет содержательной.

Глава 7, _Устранение неполадок OpenVPN-маршрутизации_, дает представление об устранении неполадок маршрутизации при настройке VPN с помощью OpenVPN. Вы узнаете, как обнаруживать, диагностировать и устранять распространенные проблемы маршрутизации.

В главе 8 _Настройка производительности_ объясняется, как можно оптимизировать производительность настройки OpenVPN. Вы узнаете, как диагностировать проблемы с производительностью и как настроить параметры OpenVPN для ускорения работы вашего VPN.

В главе 9 _Интеграция ОС_ рассматриваются тонкости интеграции OpenVPN с операционной системой, на которой он работает. Вы узнаете, как использовать OpenVPN в наиболее часто используемых клиентских операционных системах: Linux, Mac OS X и Windows.

В главе 10 _Расширенная конфигурация_ более подробно рассматриваются параметры конфигурации, которые может предложить OpenVPN. Рецепты будут охватывать как расширенные конфигурации сервера, такие как использование динамической DNS, так и расширенные конфигурации клиента, такие как использование прокси-сервера для подключения к серверу OpenVPN.

## Что вам нужно для этой книги

Чтобы извлечь максимальную пользу из этой книги, есть некоторые ожидания предшествующих знаний и опыта. Предполагается, что читатель имеет четкое представление о системном администрировании, а также знание TCP/IP сетей. Также требуются некоторые знания по установке OpenVPN, для чего вы можете обратиться к книге _Beginning OpenVPN 2.0.9_.

## Для кого предназначена эта книга

Эта книга предназначена для системных администраторов, которые имеют базовые знания OpenVPN и с нетерпением ждут, чтобы построить, защитить и управлять VPN, используя последнюю версию. Эта книга предполагает некоторые предварительные знания о сетях TCP/IP и OpenVPN. И чтобы извлечь максимум пользы из этой книги, вы должны обладать навыками сетевого администрирования.

## Конвенции

В этой книге вы найдете ряд стилей текста, которые различают различные виды информации. Вот некоторые примеры этих стилей и объяснение их значения.
Кодовые слова в тексте отображаются следующим образом: "скопируйте файл секретного ключа tls-auth из каталога /etc/openvpn/cookbook/keys."
Блок кода задается следующим образом:

```
user nobody
group nobody
persist-tun
persist-key
keepalive 10 60
ping-timer-rem
```

Когда мы хотим привлечь ваше внимание к определенной части блока кода, соответствующие строки или элементы выделяются жирным шрифтом:

```
secret secret.key 1
ifconfig 10.200.0.2 10.200.0.1
route 172.31.32.0 255.255.255.0
tun-ipv6
ifconfig-ipv6 2001:db8:100::2 2001:db8:100::1
```

Любой ввод или вывод командной строки записывается следующим образом:

```
[root@server]# openvpn --genkey --secret secret.key
```

**Новые термины** и **важные слова** выделены жирным шрифтом. Слова, которые вы видите на экране, например в меню или диалоговых окнах, появляются в тексте следующим образом: "Перейдите в **Центр управления сетями и общим доступом** и обратите внимание, что адаптер TAP находится в разделе **общедоступная сеть** и что это невозможно изменить."

**Примечание**
Предупреждения или важные заметки появляются в таком поле.

**Совет**
Советы и рекомендации выглядят так.

## Отзывы читателей

Обратная связь от наших читателей всегда приветствуется. Дайте нам знать, что вы думаете об этой книге—что вам понравилось или не понравилось. Обратная связь с читателями важна для нас, поскольку она помогает нам разрабатывать названия, которые вы действительно получите максимальную отдачу.
Чтобы отправить нам общую обратную связь, просто напишите нам по электронной почте feedback@packtpub.com, и упомяните название книги в теме Вашего сообщения.
Если есть тема, в которой у вас есть опыт, и вы заинтересованы в написании или участии в книге, смотрите наше руководство по авторству по адресу www.packtpub.com/authors.

## Поддержка клиентов
Теперь, когда вы являетесь счастливым обладателем книги Packt, у нас есть ряд вещей, которые помогут вам получить максимальную отдачу от вашей покупки.

### Загрузка примера кода

Вы можете скачать примеры файлов кода для этой книги из своей учетной записи по адресу http://www.packtpub.com если вы приобрели эту книгу в другом месте, вы можете посетить http://www.packtpub.com/support и зарегистрируйтесь, чтобы файлы были отправлены по электронной почте непосредственно вам.
Файлы кода можно загрузить, выполнив следующие действия:
    1. Войдите или зарегистрируйтесь на нашем сайте, используя свой адрес электронной почты и пароль.
    2. Наведите указатель мыши на вкладку Поддержка вверху.
    3. Нажмите на загрузки кода и ошибки.
    4. Введите название книги в поле поиска.
    5. Выберите книгу, для которой вы хотите загрузить файлы кода.
    6. Выберите из выпадающего меню, где вы приобрели эту книгу.
    7. Нажмите на кнопку загрузить код.

Вы также можете загрузить файлы кода, нажав на кнопку файлы кода на веб-странице книги на веб-сайте издательства Packt. Эту страницу можно открыть, введя название книги в поле поиска. Обратите внимание, что вам необходимо войти в свою учетную запись Packt.
После загрузки файла убедитесь, что вы разархивировали или извлекли папку, используя последнюю версию:

  * WinRAR / 7-Zip для Windows
* Zipeg / iZip / UnRarX для Mac
* 7-Zip / PeaZip для Linux

Пакет кода для книги также размещен на GitHub по адресу https://github.com/PacktPublishing/openvpncookbook. у нас также есть другие пакеты кода из нашего богатого каталога книг и видео, доступных по адресу https://github.com/PacktPublishing/. проверьте их!

## Список опечаток

Хотя мы приложили все усилия, чтобы обеспечить точность нашего контента, ошибки случаются. Если вы обнаружите ошибку в одной из наших книг—возможно, ошибку в тексте или коде, - мы будем признательны, если вы сообщите нам об этом. Поступая таким образом, вы можете спасти других читателей от разочарования и помочь нам улучшить последующие версии этой книги. Если вы обнаружите какие-либо ошибки, пожалуйста, сообщите о них, посетив http://www.packtpub.com/submit-errata, выбрав свою книгу, нажав на ссылку форма отправки ошибок и введя сведения о ваших ошибках. Как только ваши ошибки будут проверены, ваша заявка будет принята, и ошибки будут загружены на наш веб-сайт или добавлены в любой список существующих ошибок в разделе "ошибки" этого заголовка.
Чтобы просмотреть ранее отправленные ошибки, перейдите в раздел https://www.packtpub.com/books/content/support и введите название книги в поле поиска. Необходимая информация появится в разделе Errata.

## Пиратство

Пиратство защищенных авторским правом материалов в Интернете является постоянной проблемой во всех средствах массовой информации. В компании Packt мы очень серьезно относимся к защите наших авторских прав и лицензий. Если вы столкнетесь с какими-либо незаконными копиями наших работ в любой форме в Интернете, пожалуйста, немедленно сообщите нам адрес местонахождения или название веб-сайта, чтобы мы могли воспользоваться средством правовой защиты.
Пожалуйста, свяжитесь с нами по адресу copyright@packtpub.com со ссылкой на подозрительный пиратский материал.
Мы ценим вашу помощь в защите наших авторов и нашу способность предоставить вам ценный контент.

## Вопросы

Если у вас возникли проблемы с каким-либо аспектом этой книги, вы можете связаться с нами по адресу questions@packtpub.com, и мы сделаем все возможное, чтобы решить эту проблему.
