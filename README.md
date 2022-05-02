# YouTube Radio CLI
Данный гайд написан для запуска своего радио под Linux имея небольшие мощности, например, на VPS. <br>

Минимальные требования:<br>
Одно ядро на 2ГГц<br>
512 озу<br>
Накопитель будет зависесть уже от ваших запросов к количеству треков.<br>
Максимальные же требования не ограничены. Больше ресурсов - выше качество.<br>

Подготовка:<br>
1. Установка ffmpeg<br>

Нужно уставновить свежий ffmpeg из репозитория вышего дистрибутива.<br>
debian based ```sudo apt install ffmpeg```<br>
arch based ```sudo pacman -S ffmpeg```<br>
2. Установка MPD<br>

MPD - непосредственно плеер, который будет готовить нам поток для трансляции, а MPC - консольный клиент для управления плеером.<br>
debian based ```sudo apt install mpd mpc```<br>
arch based ```sudo pacman -S mpd mpc```<br>
3. Клонируем репу моего товарища, который довел до ума мой [скрипт](https://github.com/Velaron/bds-radio)<br>
И устанаваливаем зависимости ```pip install -r requirements.txt```<br>

Настройка:<br>
Настройте MPD конфиг под себя, образец лежит в репозитории, его расположение ```/etc/mpd.conf```<br>
После этого перезапустите mpd sudo ```service restart mpd```, если нет ошибок, то идем дальше<br>
Теперь переименуем и откроем ```config.json.example``` в ```config.json```<br>
Подробнее о содержании конфига <br>
 ``` youtube_key``` - ключ трансляции, берем на youtube<br>
  ```audio_url``` - ссылка на ваш аудиопоток из mpd<br>
  ```background_params``` - настройки фона трансляции<br>
  ```text_params``` - настройка текста трека на фоне трансляции, цвет, размер, шрифт<br>
  ```output_params``` - настройка вывода трансляции битрейт, кодеки для аудио и видео<br>
  
Запуск:<br>
Добавим треки в mpd<br>
```mpc --host yourmpdpass@localhost add``` /<br>
```mpc --host yourmpdpass@localhost play```<br>

Идем в папку со скрипотм и запускаем скрипт<br>
```python bds-radio.py```<br>
если же стрим пошел, то можно запускать в фоне, установим screen<br>
```sudo apt install screen```<br>

И теперь финальный запуск ```screen -d -m python bds-radio.py```<br>
