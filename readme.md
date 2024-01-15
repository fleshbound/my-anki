## гайд

### подготовка

! Необходимо наличие: Ubuntu 22.04, pdflatex, convert (imagemagick)

1. Установите [Anki](https://docs.ankiweb.net/platform/linux/installing.html) (на момент написания у меня стоит 23.10.1 на qt6)
2. Установите [аддон для изменения процесса сборки](https://ankiweb.net/shared/info/937148547) (копируем цифры, Anki -> Tools -> Add-ons -> Get Add-ons -> вставляем)
3. Выбираем этот аддон и открываем его файлы (View Files)
4. Копируем куда-нибудь старую версию \_\_init\_\_.py, создаем новую с кодом, представленным ниже
```py
newLaTeX = \
[
    ["pdflatex", "-interaction=nonstopmode", "--shell-escape", "tmp.tex"],
    ["convert", "-density", "200", "-trim", "tmp.pdf", "tmp.png"]
]
import anki.latex
anki.latex.latexCmds = newLaTeX
```
5. Перезапускаем anki
6. Загружаем необходимую колоду
7. Пробуем открыть карточки???

### полезные заметки

- очень часто может быть путаница из-за смешанных фигурных скобок (}}, }) --- старайтесь сначала разделять их пробелами по смыслу, а потом убирать их, если это влияет на внешний вид;
- Ctrl+T + Е
- ```\[ \]``` --- Mathjax вставка формулы, ее нельзя нормально скопировать, зато есть моментальное превью (окружение equation* лучше в большинстве случаев, на мой взгляд)
- ``\limits``` --- для красивых пределов

### немного о типах карточек

#### Basic LaTeX

ну, просто бейсик. нельзя вставить картинки без изворотов

#### Basic LaTeX (and reversed card)

ну, просто бейсик. + бейсик наоборот (автоматически)

#### Basic LaTeX graphics

ну, просто бейсик. + можно вставлять картинки

Команда (пример использования --- самый оптимальный):
```
\includeimage{filename}{f}{h}{0.5\textwidth}
```

Для того, чтобы работало корректно:
1. Куда-то лезем
```
Anki -> Tools -> Manage Note Types -> Basic LaTeX graphics -> Options
```
2. Заменяем в строке с командой ```\graphicspath``` путь на желаемый (путь к картинкам).
3. Перезапускаем, все дела

#### Cloze LaTeX

Все аналогично но нет второго поля: на карточках необходимо скрыть часть текста с помощью конструкции ```{{c1::я хочу скрыть этот текст}}```, где 1 --- номер "карточки скрывания". В общем, интуитивно понятно.

key: ctrl+alt+shift+c, ctrl+shift+c
