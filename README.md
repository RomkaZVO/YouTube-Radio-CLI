# YouTube Radio CLI
Данный гайд написан для запуска своего радио под Linux имея небольшие мощности, например, на VPS.

Минимальные требования:
Одно ядро на 2ГГц
512 озу
Накопитель будет зависесть уже от ваших запросов к количеству треков.
Максимальные же требования не ограничены. Больше ресурсов - выше качество.

Подготовка:
1. Установка ffmpeg

Нужно уставновить свежий ffmpeg из репозитория вышего дистрибутива.
debian based sudo apt install ffmpeg
arch based sudo pacman -S ffmpeg
2. Установка MPD

MPD - непосредственно плеер, который будет готовить нам поток для трансляции, а MPC - консольный клиент для управления плеером.
debian based sudo apt install mpd mpc
arch based sudo pacman -S mpd mpc
3. Клонируем репу моего товарища, который довел до ума мой скрипт.

https://github.com/Velaron/bds-radio
И устанаваливаем зависимости pip install -r requirements.txt

Настройка:
Настройте MPD конфиг под себя, образец лежит в репозитории, его расположение /etc/mpd.conf
После этого перезапустите mpd sudo service restart mpd, если нет ошибок, то идем дальше
Теперь переименуем и откроем config.json.example в config.json
Подробнее о содержании конфига 
  youtube_key - ключ трансляции, берем на youtube
  audio_url - ссылка на ваш аудиопоток из mpd
  background_params - настройки фона трансляции
  text_params - настройка текста трека на фоне трансляции, цвет, размер, шрифт
  output_params - настройка вывода трансляции битрейт, кодеки для аудио и видео
  
Запуск:
Добавим треки в mpd
mpc --host yourmpdpass@localhost add /
mpc --host yourmpdpass@localhost play

Идем в папку со скрипотм и запускаем скрипт
python bds-radio.py
если же стрим пошел, то можно запускать в фоне, установим screen
sudo apt install screen

и теперь финальный запуск screen -d -m python bds-radio.py
