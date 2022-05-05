Приложение вырезает прямоугольник из BMP-файла с изображением,
поворачивает этот прямоугольник на 90 градусов по часовой стрелке и сохраняет результат в отдельный
файл.

Все изображения (изначальное для чтения и сохранённый результат) хранятся в заданном формате:

* Общий формат — [BMP](https://ru.wikipedia.org/wiki/BMP).
* В рамках формата BMP используется формат *DIB* с заголовком `BITMAPINFOHEADER` (версия 3).
* Значение поля `biHeight` (высота изображения) строго больше нуля.
* Используются 24 бита цвета на пиксель (один байт на цветовой канал).
* Палитра (таблица цветов) не используется.
* Сжатие не используется.

### Консольное приложение
Приложение запускается следующей командой:

```
./hw-01_bmp crop-rotate ‹in-bmp› ‹out-bmp› ‹x› ‹y› ‹w› ‹h›
```

Используемые параметры:

* `crop-rotate` — обязательный параметр, означающий выполняемое действие.
* `in-bmp` — имя входного файла с изображением.
* `out-bmp` — имя выходного файла с изображением.
* `x`, `y` — координаты левого верхнего угла области, которую необходимо вырезать и повернуть.
  Координаты начинаются с нуля, таким образом *(0, 0)* — это верхний левый угол.
* `w`, `h` — соотвественно, ширина и высота области до поворота.

Таким образом, если обозначить ширину и высоту исходного изображения за `W` и `H`, соответственно,
для корректных аргументов верны следующие неравенства:

* `0 <= x < x + w <= W`
* `0 <= y < y + h <= H`


В дополнение к команде `crop-rotate` есть команды `insert` и `extract`,
позволяющие спрятать внутри изображения сообщение
([стеганография](https://ru.wikipedia.org/wiki/%D0%A1%D1%82%D0%B5%D0%B3%D0%B0%D0%BD%D0%BE%D0%B3%D1%80%D0%B0%D1%84%D0%B8%D1%8F)).
Команда `insert` сохраняет в изображение сообщение, а `extract` — извлекает его оттуда.


### Способ кодирования
Исходное сообщение состоит только из заглавных латинских букв, пробела, точки и запятой.

Для передачи сообщения, помимо изображения-носителя, потребуется __ключ__ — текстовый файл,
описывающий, в каких пикселях кодируются биты сообщения.
В этом файле на отдельных строчках записаны:

* Координаты `x` и `y` (`0 <= x < W`, `0 <= y < H`) пикселя, в который надо сохранить
  соответствующий бит.
* Буква `R`/`G`/`B` обозначающая цветовой канал, в младшем бите которого требуется записать бит
  сообщения.

### Консольное приложение
Для сохранения секретной строчки в изображение приложение запускается следующей командой:
```
./hw-01_bmp insert ‹in-bmp› ‹out-bmp› ‹key-txt› ‹msg-txt›
```

Для извлечения секретной строчки из изображения приложение запускается следующей командой:
```
./hw-01_bmp extract ‹in-bmp› ‹key-txt› ‹msg-txt›
```

Используемые параметры:

* `in-bmp` — имя входного файла с изображением.
* `out-bmp` — имя выходного файла с изображением.
* `key-txt` — тестовый файл с ключом.
* `msg-txt` — текстовый файл с секретным сообщением.