---
name: anime-short-film
description: Превращает одну фразу идеи в короткий аниме-фильм для генерации. Пишет историю по сценам, промпты картинок-референсов (герой, локация, каждый предмет), чтобы они не менялись от кадра к кадру, и мастер-промпт для видео с таймкодами, закреплённым стилем (style lock) и ссылками @image1..N. Подходит для Google Flow (Veo, Omni) и Seedance 2.0. Длинный фильм режет на клипы с общими референсами. Используй, когда просят «аниме-ролик», «короткий мультфильм», «анимированный фильм из идеи», «рисованный ролик для бренда», «промпт для Veo/Seedance по сценам».
---

# Короткий аниме-фильм из одной фразы

Скилл ведёт от одной строки идеи до готового набора для генерации:

1. история по сценам;
2. промпты картинок-референсов: герой, локация, каждый важный предмет;
3. мастер-промпт для видео с таймкодами, style lock и ссылками на референсы @image1..N.

Сами картинки и видео скилл не рендерит. Он выдаёт тексты, которые человек вставляет в генератор картинок, а потом в Flow или Seedance.

## Когда использовать

- Человек дал идею одной-двумя фразами и хочет из неё ролик.
- Нужен рисованный (аниме, гуашь, акварель) ролик, где герой одинаковый во всех кадрах.
- Нужен промпт для Veo, Omni или Seedance 2.0 с таймкодами по кадрам.
- Есть готовые референсы, и нужно собрать к ним мастер-промпт.

Не используй для фотореалистичной рекламы с живыми людьми и для роликов с говорящей головой: там другие правила промптов.

## Что спросить перед стартом

Если человек этого не сказал, задай вопросы ОДНИМ сообщением и предложи значения по умолчанию. Ответил «как скажешь» или промолчал, бери умолчания.

- Длина фильма: по умолчанию 30 секунд.
- Формат кадра: по умолчанию 9:16, вертикаль для Reels, Shorts и TikTok.
- Генератор видео: по умолчанию Seedance 2.0.
- Стиль: по умолчанию рисованное аниме в духе классических японских полнометражных мультфильмов, блок STYLE BLOCK по умолчанию ниже.
- Текст в кадре: по умолчанию его нет, кроме финальной карточки в ролике бренда.
- Бренд, логотип или продукт: по умолчанию без них.
- Звук: по умолчанию атмосферные шумы и музыка без слов.

## Длина клипа и нарезка

Генераторы делают видео кусками ограниченной длины. Лимиты меняются, поэтому перед нарезкой спроси человека, какой максимум он видит в интерфейсе. Если не знает, бери эти рабочие значения:

- Google Flow, модель Veo: клипы короткие, точную длину смотри в интерфейсе; пока не проверил, считай 8 секунд. Референсы идут ингредиентами, до 3 картинок.
- Google Flow, модель Omni: по документации Google до 15 секунд и до 6 картинок-референсов; в Flow сверь с настройкой длины.
- Seedance 2.0: клип от 4 до 15 секунд, принимает несколько картинок-референсов, обращение к ним через @image1, @image2 и дальше.

Правило нарезки:

1. `clip_max` = безопасная длина клипа выбранного генератора.
2. Фильм длиной не больше `clip_max` идёт одним клипом.
3. Длиннее: число клипов = длина фильма, делённая на `clip_max`, с округлением вверх. Режь только на границе сцены, чтобы действие внутри кадра не рвалось.
4. Все клипы получают ОДИН И ТОТ ЖЕ блок style lock и одни и те же референсы с теми же номерами @image.
5. Каждый следующий клип начинается с описания последнего кадра предыдущего (поза героя, место, свет). Если генератор умеет брать первый кадр, человек кладёт туда стоп-кадр конца прошлого клипа.
6. Таймкоды внутри каждого клипа начинаются с 0.0. Общий таймкод фильма пиши отдельно в шапке клипа.

## Шаги

### Шаг 1. Логлайн и бит истории

Из фразы человека напиши:

- логлайн одной строкой: кто, что делает, чем кончается;
- три бита: завязка, движение, финал (эмоциональная точка, ради которой смотрят).

Не добавляй героев и сюжетных линий, которых нет во фразе. Короткий фильм держится на одном действии.

### Шаг 2. Сцены и кадры

Раздели фильм на кадры (shots). Ориентир: один кадр на 2.5-4 секунды. Для 30 секунд это 8-10 кадров.

Для каждого кадра укажи:

- номер и таймкод (начало-конец в секундах, с десятыми);
- крупность: общий, средний, крупный, деталь;
- движение камеры: статика, панорама, проезд, следование за героем;
- что происходит, одним-двумя предложениями;
- какие референсы в кадре (@image-номера).

Правила кадров:

- Таймкоды идут встык, без дыр и наложений, сумма равна длине клипа.
- В одном кадре одно действие.
- Каждые 2-3 кадра меняй крупность, иначе ролик выглядит как слайд-шоу.
- Финальный кадр держи на 0.5-1 секунду дольше остальных.

### Шаг 3. Список ассетов

Составь список всего, что должно выглядеть одинаково в разных кадрах:

- герой (и второй персонаж, если он есть во фразе);
- главная локация (одна, максимум две);
- каждый предмет, который виден крупно или с которым герой что-то делает;
- логотип или продукт, если это ролик бренда.

Каждому ассету присвой номер @image по порядку. Сначала герой, потом локация, потом предметы. Если генератор принимает меньше картинок, чем ассетов, объедини мелкие предметы в один лист (например, «скейт и рюкзак на одном листе»).

### Шаг 4. Промпты картинок-референсов

Для каждого ассета один промпт. Промпты пиши на английском: генераторы картинок понимают его точнее. Все промпты начинаются с одного и того же блока стиля (STYLE BLOCK), чтобы картинки были из одного мира.

**STYLE BLOCK по умолчанию.** Берёшь его, если человек не попросил другой стиль. Это узнаваемый рисованный стиль японских полнометражных мультфильмов, описанный приметами. Имена студий и режиссёров в промпт не пишешь никогда, только приметы.

```
Hand-painted 2D anime film look, lush gouache-painted backgrounds with visible brush texture, soft warm natural light, big fluffy cumulus clouds in a deep blue sky, simple clean line art for faces with small expressive features, gentle greens and warm earth tones, soft cel shading, calm steady camera with slow pans and long quiet holds, peaceful everyday atmosphere.
```

К блоку можно дописать время суток и свет конкретного фильма, например «warm summer evening, golden hour».

**Герой: лист персонажа (character sheet).**
- Нейтральный светлый фон, без окружения.
- 3-4 вида в ряд: спереди, три четверти, сбоку, сзади. В полный рост.
- Отдельно крупно лицо и ключевые детали одежды и аксессуаров.
- Конкретные приметы: возраст, причёска и цвет волос, цвет глаз, одежда по слоям с цветами, обувь, аксессуары. Пиши цвета словами («faded cobalt blue»), без «нарядный», «красивый».
- Эти же приметы дословно повторяются потом в видео-промпте.

**Локация: плита сцены (scene plate).**
- Без людей.
- 2-4 ракурса одного места: общий план, план с уровня глаз героя, деталь.
- Время суток и свет те же, что в фильме.

**Предмет: лист предмета.**
- Нейтральный фон, 3-4 ракурса.
- Цвета, материал, потёртости, надписи, если они важны.

**Логотип или продукт (только для бренда).**
- Чистое изображение на нейтральном фоне, без искажений.

### Шаг 5. Мастер-промпт для видео

Один промпт на клип по шаблону ниже. Пиши на английском. Обязательные части:

1. Строка таймингов: сколько кадров, сколько секунд, таймкод каждого кадра, тип склеек.
2. Список референсов: @image1 это кто или что.
3. STYLE LOCK: стиль, свет, палитра, фактура, что запрещено. Блок одинаковый во всех клипах фильма.
4. CHARACTER LOCK: приметы героя дословно из промпта референса.
5. Кадры по таймкодам: `Shot N (a.a-b.b s): ...`.
6. ON-SCREEN TEXT: отдельной строкой, запрещён ли текст в кадре и где он разрешён.
7. AUDIO: звуки и музыка, без слов, если человек не просил речь.

Для Flow (Veo, Omni) референсы человек загружает в проект и подключает к генерации. Обращения @image оставь в промпте и добавь в начало строку «Reference images: image 1 = ..., image 2 = ...», чтобы связь была понятна и без синтаксиса @.

### Шаг 6. Проверка перед выдачей

Пройди чек-лист и исправь, если что-то не так:

- [ ] Таймкоды каждого клипа идут встык от 0.0 до длины клипа.
- [ ] Каждый клип не длиннее `clip_max`.
- [ ] Каждый ассет из списка имеет промпт и номер @image, номера совпадают во всех клипах.
- [ ] STYLE LOCK и CHARACTER LOCK одинаковые во всех клипах, символ в символ.
- [ ] В кадрах нет предметов и персонажей, которых нет в референсах (кроме фона и массовки).
- [ ] Нет имён реальных студий, режиссёров и художников: генераторы отклоняют такие промпты. Стиль описан словами.
- [ ] Текст в кадре либо запрещён, либо описан точно: какие слова, где, каким шрифтом, сколько секунд.

## Шаблоны вывода

Выдавай результат в этом порядке и с этими заголовками.

### 1. История

```
Логлайн: <одна строка>
Длина: <N> с, формат <9:16>, генератор <Seedance 2.0>, клипов: <K>

Завязка: <кто герой, где он и что сейчас начнёт делать>.
Движение: <как развивается действие, что герой видит по дороге>.
Финал: <эмоциональная точка, на которой фильм заканчивается>.
```

### 2. Раскадровка

Каждый кадр одной строкой: номер, таймкод, крупность и камера, действие, референсы.

```
Клип 1 (фильм 0.0-15.0 с)
Shot 1 | 0.0-3.0 | общий, статика | <что происходит в кадре, одним предложением> | @image2
Shot 2 | 3.0-6.0 | средний, следование | <что делает герой в этом кадре> | @image1 @image3
<и так до последнего кадра клипа, таймкоды встык>
```

### 3. Референсы

Сначала общий блок стиля, потом по одному промпту на каждый ассет.

```
STYLE BLOCK (начало каждого промпта картинки):
<hand-painted anime style ...>

@image1 Герой, лист персонажа
<промпт>

@image2 Локация, плита сцены
<промпт>

@image3 <Предмет>, лист предмета
<промпт>
```

### 4. Мастер-промпт видео (на каждый клип)

```
CLIP <k> of <K>. <S> shots across <D> seconds. Shot 1 runs 0.0-3.0s, shot 2 runs 3.0-6.0s, ... Hard cuts between shots, no transitions, no dissolves, no fades. No slow motion, no speed ramps.

Reference images: @image1 = <hero> character sheet, @image2 = <location> scene plate, @image3 = <object> sheet.

STYLE LOCK: <одинаковый во всех клипах блок стиля>. Every frame keeps this exact style. No 3D render, no photorealism, no CGI look, no style drift between shots.

CHARACTER LOCK: the boy from @image1 in every shot: <приметы дословно>. Same face, same hair, same clothes and colors in every shot. No extra characters except distant background people.

Shot 1 (0.0-3.0s): <крупность>, <движение камеры>. <действие героя в кадре>.
<одна строка на каждый следующий кадр клипа, в том же формате>

CONTINUITY: <для клипа 2 и дальше: clip starts exactly where previous clip ended: поза, место, свет>.

ON-SCREEN TEXT: no text, no captions, no subtitles, no logos, no watermarks anywhere in frame.

AUDIO: <звуки и музыка>. No dialogue, no voiceover, no singing.
```

### 5. Как собрать

Короткий список для человека: какие картинки сгенерировать первыми, какие из них загрузить в каком порядке, какой промпт вставить, какую длину и формат выставить.

## Пример

Идея: «мальчик на скейте катится по лестнице к морю летним вечером».

Параметры: 30 секунд, 9:16, Seedance 2.0 (клип до 15 с), значит 2 клипа по 15 секунд.

### 1. История

```
Логлайн: Мальчик на скейте летит вниз по бесконечной лестнице приморского городка и на закате выкатывается к морю.
Длина: 30 с, формат 9:16, генератор Seedance 2.0, клипов: 2

Завязка: летний вечер, мальчик встаёт на скейт на вершине каменной лестницы над морем.
Движение: он катится по пролётам и узким переулкам, мимо белья на верёвках, кошек и черепичных крыш, море то появляется, то пропадает.
Финал: последний пролёт выводит его на набережную, он тормозит и смотрит на закатное море.
```

### 2. Раскадровка

Десять кадров, по пять в каждом клипе, таймкоды каждого клипа считаются от нуля.

```
Клип 1 (фильм 0.0-15.0 с)
Shot 1 | 0.0-3.0 | общий сверху, статика | городок на холме, лестница вниз к морю, солнце низко | @image2
Shot 2 | 3.0-5.5 | деталь, статика | кеды встают на дек скейта, рюкзак качается | @image1 @image3
Shot 3 | 5.5-8.5 | средний, следование сзади | мальчик отталкивается и катится вниз по пологому пролёту | @image1 @image3 @image2
Shot 4 | 8.5-11.5 | общий сбоку, панорама | он проносится под верёвками с бельём, кошка поднимает голову | @image1 @image2
Shot 5 | 11.5-15.0 | средний спереди, проезд назад | ветер в волосах, между домами впереди открывается море | @image1 @image3

Клип 2 (фильм 15.0-30.0 с)
Shot 1 | 0.0-3.0 | средний спереди, проезд назад | продолжение: мальчик катится навстречу камере, море за домами | @image1 @image3 @image2
Shot 2 | 3.0-5.5 | деталь, следование | колёса стучат по стыкам каменных плит | @image3 @image2
Shot 3 | 5.5-8.5 | общий сверху, статика | маленькая фигурка на последнем пролёте, впереди набережная и закат | @image2
Shot 4 | 8.5-11.0 | средний сбоку | он тормозит у парапета, скейт разворачивается | @image1 @image3
Shot 5 | 11.0-15.0 | общий со спины, медленный наезд | мальчик стоит у моря, солнце касается воды | @image1 @image2
```

### 3. Референсы

Три картинки: лист героя, плита локации и лист скейта, все с одним блоком стиля.

```
STYLE BLOCK:
Hand-painted 2D anime film look, lush gouache-painted backgrounds with visible brush texture, soft warm natural light, big fluffy cumulus clouds in a deep blue sky, simple clean line art for faces with small expressive features, gentle greens and warm earth tones, soft cel shading, calm steady camera with slow pans and long quiet holds, peaceful everyday atmosphere, warm summer evening, golden hour, cinematic composition.

@image1 Герой, лист персонажа
[STYLE BLOCK] Character sheet of a 12-year-old boy on a plain light beige background. Four full-body views in a row: front, three-quarter, side, back. Messy chestnut-brown hair, big dark-brown eyes, light freckles across the nose. Faded cobalt-blue short-sleeve shirt worn open over a white t-shirt, rolled sand-colored shorts, white canvas sneakers with red laces, mustard-yellow canvas backpack with two front pockets. Separate close-up of the face and of the sneakers. Consistent proportions, no background scenery, no text.

@image2 Локация, плита сцены
[STYLE BLOCK] Scene plate of a small Mediterranean seaside town on a steep hill, no people. Long stone staircase winding down between whitewashed houses with terracotta roofs, laundry lines, potted plants, the sea visible at the bottom, golden hour sun low over the water, a few big white cumulus clouds. Three panels: wide view from the top of the stairs, eye-level view on a mid flight of stairs, close-up of worn stone steps. No text.

@image3 Скейт, лист предмета
[STYLE BLOCK] Object sheet of a skateboard on a plain light beige background, four views: top of the deck, bottom of the deck, side view, three-quarter view. Wooden deck painted orange with a hand-painted sea and clouds graphic on the bottom, worn edges, chunky red wheels, silver trucks. No text.
```

### 4. Мастер-промпт видео, клип 1

```
CLIP 1 of 2. 5 shots across 15 seconds. Shot 1 runs 0.0-3.0s, shot 2 runs 3.0-5.5s, shot 3 runs 5.5-8.5s, shot 4 runs 8.5-11.5s, shot 5 runs 11.5-15.0s. Hard cuts between shots, no transitions, no dissolves, no fades. No slow motion, no speed ramps. Vertical 9:16.

Reference images: @image1 = boy character sheet, @image2 = seaside town staircase scene plate, @image3 = skateboard sheet.

STYLE LOCK: Hand-painted 2D anime film look, lush gouache-painted backgrounds with visible brush texture, soft warm natural light, big fluffy cumulus clouds in a deep blue sky, simple clean line art for faces with small expressive features, gentle greens and warm earth tones, soft cel shading, calm steady camera with slow pans and long quiet holds, peaceful everyday atmosphere, warm summer evening, golden hour. Every frame keeps this exact style. No 3D render, no photorealism, no CGI look, no style drift between shots.

CHARACTER LOCK: the boy from @image1 in every shot: 12 years old, messy chestnut-brown hair, dark-brown eyes, light freckles, faded cobalt-blue open shirt over a white t-shirt, sand-colored shorts, white sneakers with red laces, mustard-yellow backpack. He rides the skateboard from @image3: orange deck, red wheels. Same face, hair, clothes and colors in every shot. No extra characters except one cat and distant background people.

Shot 1 (0.0-3.0s): wide high-angle static shot of the town from @image2, stone staircase falling toward the sea, sun low over the water.
Shot 2 (3.0-5.5s): close-up, static. White sneakers with red laces step onto the orange deck, the yellow backpack swings into frame.
Shot 3 (5.5-8.5s): medium shot, camera follows from behind. The boy pushes off and rolls down a gentle flight of stone stairs.
Shot 4 (8.5-11.5s): wide side shot, camera pans with him. He passes under laundry lines, a cat on a wall lifts its head.
Shot 5 (11.5-15.0s): medium front shot, camera tracks backward. Wind in his hair, he smiles, between the houses ahead the sea opens up in golden light.

ON-SCREEN TEXT: no text, no captions, no subtitles, no logos, no watermarks anywhere in frame.

AUDIO: skateboard wheels rolling on stone, distant seagulls, light warm piano and strings. No dialogue, no voiceover, no singing.
```

### 4. Мастер-промпт видео, клип 2

```
CLIP 2 of 2. 5 shots across 15 seconds. Shot 1 runs 0.0-3.0s, shot 2 runs 3.0-5.5s, shot 3 runs 5.5-8.5s, shot 4 runs 8.5-11.0s, shot 5 runs 11.0-15.0s. Hard cuts between shots, no transitions, no dissolves, no fades. No slow motion, no speed ramps. Vertical 9:16.

Reference images: @image1 = boy character sheet, @image2 = seaside town staircase scene plate, @image3 = skateboard sheet.

STYLE LOCK: Hand-painted 2D anime film look, lush gouache-painted backgrounds with visible brush texture, soft warm natural light, big fluffy cumulus clouds in a deep blue sky, simple clean line art for faces with small expressive features, gentle greens and warm earth tones, soft cel shading, calm steady camera with slow pans and long quiet holds, peaceful everyday atmosphere, warm summer evening, golden hour. Every frame keeps this exact style. No 3D render, no photorealism, no CGI look, no style drift between shots.

CHARACTER LOCK: the boy from @image1 in every shot: 12 years old, messy chestnut-brown hair, dark-brown eyes, light freckles, faded cobalt-blue open shirt over a white t-shirt, sand-colored shorts, white sneakers with red laces, mustard-yellow backpack. He rides the skateboard from @image3: orange deck, red wheels. Same face, hair, clothes and colors in every shot. No extra characters except distant background people.

CONTINUITY: the clip starts exactly where clip 1 ended: the boy rolling toward camera on a mid flight of stairs, sea visible between the houses behind him, golden hour light.

Shot 1 (0.0-3.0s): medium front shot, camera tracks backward. The boy keeps rolling toward camera, the sea glowing between the houses.
Shot 2 (3.0-5.5s): close-up, camera follows low. Red wheels clatter over the joints of worn stone slabs.
Shot 3 (5.5-8.5s): wide high-angle static shot. A small figure on the last flight of stairs, the seafront promenade and the setting sun ahead.
Shot 4 (8.5-11.0s): medium side shot. He brakes at the stone parapet, the skateboard swings sideways and stops.
Shot 5 (11.0-15.0s): wide shot from behind, slow push-in. The boy stands at the parapet holding the skateboard, the sun touches the sea, warm light on the water.

ON-SCREEN TEXT: no text, no captions, no subtitles, no logos, no watermarks anywhere in frame.

AUDIO: wheels on stone, then quiet waves and seagulls, the piano theme resolves softly at the end. No dialogue, no voiceover, no singing.
```

### 5. Как собрать

Порядок действий для этого примера, по шагам, от картинок до готового ролика:

```
1. Сгенерируй @image1, @image2, @image3 по промптам. Выбери по одному лучшему варианту каждого.
2. В Seedance 2.0 загрузи их строго в этом порядке: герой, локация, скейт.
3. Формат 9:16, длина 15 с. Вставь мастер-промпт клипа 1, сгенерируй.
4. Сохрани последний кадр клипа 1. Для клипа 2 загрузи те же три картинки в том же порядке (и последний кадр как первый, если генератор это позволяет), вставь промпт клипа 2.
5. Склей клипы в любом монтажном приложении.
```

## Если генератор ушёл в сторону

- Герой поменял лицо или одежду: усиль CHARACTER LOCK, перечисли приметы ещё раз внутри проблемного кадра, проверь, что @image1 загружен первым.
- Стиль стал 3D или фото: добавь в STYLE LOCK запреты «no 3D, no photorealism» ещё раз в конец промпта.
- Таймкоды поплыли: сократи число кадров в клипе, на 8 секунд хватает 3 кадров, на 15 секунд 5-6.
- Появились надписи: строка ON-SCREEN TEXT должна быть в промпте отдельным абзацем.
- Лишние люди или предметы: добавь в кадр «only the boy, no other characters».
