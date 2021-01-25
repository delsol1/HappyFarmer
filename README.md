# Happy Farmer #

## Вводная часть

***О скрипте.***   

Скрипт создан для абуза @Litecoin_click_bot в Telegram. Если приложить немного усилий, его можно адаптировать под работу с @BTC_click_bot, @BCH_click_bot, @Doge_click_bot.  
Но, как я убедился на практике, это бесполезно. Нормально платят только в @Litecoin_click_bot.   

***Архитектура проекта.***  

В общих чертах расскажу об архитектуре поекта. Как вы могли заметить, весь код разбит на несколько файлов: ```start.py, main.py, func.py```. Так же, при запуске скрипта, будут созданы файлы  ```telegram_farm.db``` и ```telegram_farm.db```.    

```start.py``` - запускает работу срипта и перезапускает его, если он по  каким-либо причинам упал.  

```main.py``` содержит в себе функцию-контроллер скрипта. С помощью этого контроллера пользователь осуществляет взаимодействие со скриптом.

```func.py``` - это "мозг" скрипта. В файле находятся все функции, необходимые для абуза @Litecoin_click_bot.  

```telegram_farm.db``` - база данных/

```TelegramFarmErrors.log``` - файл-лог, куда заносятся отчёты о банах аккаунтов и прочих неприятностях.

***Обратная связь.*** Есть предложения по улучшению проекта? Естьзамечани по коду? Возникли вопросы? Пишите мне в   VK: https://vk.com/mtchuikov или Telegram: https://t.me/mtchuikov.  

***Поддержать автора.***  
BNB (bep20): 0xa4ca77291e6a7532d527b0d3efbe265ae4eceec0  
TRX: TTdXB7RbydKQpxs3wXJx4GBm9r9EqKuBaW  
LTC: Lgp4w1ubkAgcQEVVBSiAN788FUHmZyh5c9  
Qiwi nickname: MTCHUIKOV

## Мануал по работе со скриптом

***Предварительная подготовка.***

```Шаг 1.``` Устанавливаем интерпретатор Python.  
Инструкция по установке Python https://python-scripts.com/install-python Запоминаем папку, где находится
интерпретатор, это пригодится в дальнейшем (по умолчанию Python устанавливается по следующему пути  
C:\Users\Имя_Пользователя\AppData\Local\Programs\Python\Python39\python.exe).

---

```Шаг 2.``` Устанавливаем PIP (python installer packagea).   
Инструкция по сутановке PIP: https://pythonru.com/baza-znanij/ustanovka-pip-dlja-python-i-bazovye-komandy  

---

```Шаг 3.``` Скачиваем файлы из репозитория.    
Делается это следующим образом: на странице проекта нажимаем кнопку "Code" => "Download ZIP". Скачанный 
архив распаковываем в папку.

---

```Шаг 4.``` Указываем путь до интерпритатора Python в скрипте.  
Заходим в папку, где находится скаченный проект (для удобства буду называть эту папку folderHappyFarmer).  
Открываем файл ```start.py```. В верху файла есть строчка код, которая указывает на путь до интерпретатора: ```#!C:\Users\Misha\AppData\Local\Programs\Python\Python39\python.exe```. Нужно удалить всё, до #! и записать
свой путь.

---

```Шаг 5.``` Установка пакетов.  
Нажимаем сочетание клавиш WIN + R, прописываем cmd. Открывается консоль Windows. В консоле прописываем команды:  
```pip install telethon```  
```pip install requests```  
```pip install selenium```    
```pip install pycoingecko```  
```pip3 install bs4```  
```pip3 install lxml```

---

```Шаг 6.``` Установка Goolge Chrome и ChromeDriver.    
Гугл, надеюсь, есть у всех. Но кроме гугла необходим ChromeDriver нужной версии. Скачать его можно по ссылку https://chromedriver.chromium.org/downloads. Что бы узнать нужную версию ChromeDriv: открываем гугл => "Настройки" => "О браузере".
Запоминаем версию хрома, для такой же версии. Загруженный ChromeDriver кидаем в нашу папочку folderHappyFarmer.

---

```Шаг 6.``` Указываем путь до ChromeDriver в скрипте.  
С помощью блокнота открываем файл func.py  Ищем строку кода  
```browserChrome = webdriver.Chrome(r'C:\Users\Misha\Desktop\folderHappyFarmer\chromedriver.exe',options=chromeOptions)``` В место  
```C:\Users\Misha\Desktop\bot_v2\chromedriver.exe``` указываем свой путь до ChromeDriver.

---

Предварительная подготовка закончена, поздравляю.

***Работа со скриптом.***  

```Шаг 1.``` Запуск скрипта.  
Делается это через консоль Windows: ```cd C:\Users\Misha\Desktop\folderHappyFarmer\``` (т.е. указываем путь до папки со скриптом).  
Пишем команду: ```python start.py```. Скрипт запущен.

---

```Шаг 2.``` Управление скриптом. Описание комманд.  

./addData - активирует функцию добавления данных в БД. На ввод принемает следующие данные: номер телефона, api id, api hash. Последние создаются на сайте https://my.telegram.org/auth в разделе API.

./settings - перекидывает в раздел "Настройки". Появляется вложенный список комманд:
    
   ./addRefCode - принимаеь на вход реферальный код от @Litecoin_click_bot (например, моя реферальныя ссылка в боте https://t.me/Litecoin_click_bot?start=T8bVS,
   значит, мой реферальный код T8bVS). Реферальный код указывается от 1 аккаунта. По реферальной ссылке этого аккаунта будут зарегестрированны все остальные   
   аккаунты.
    
   ./updRefCode - обновляет реферальный код (если аккаунт забанили и т.п.)
    
   ./addBlockIoApiKey - принимает на вход Api ключ от Litecoin кошелька с сайта https://block.io/. На этом сайте будут создавать Litecoin кошельки для вывода.
   
   ./updBlockIoApiKey - обновляет Api ключ.
   
   ./back - назад в главное меню.

./createSession - создаёт сессию телеграм. Для создания нужно будет ввести код из приложения.

./subBot - запускает @Litecoin_click_bot на всех аккаунтах.

./startFarming - запуск фарминга.

./checkBalance - проверка баланса.

./withdrawBalance - вывод с баланса бота.






