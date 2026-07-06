# Домашнее задание к занятию «Инструменты Git»
Выполнил: Береснев Игорь Андреевич

---

## 1. Коммит с хешем, начинающимся на aefea

**Как получено:**
Для поиска коммита по началу хеша использована команда `git log --oneline`, которая выводит сокращённые хеши (первые 7-10 символов) и комментарии. С помощью `grep "^aefea"` отфильтрованы строки, начинающиеся с `aefea`.

**Команда:**
```bash
git log --oneline | grep "^aefea"
```

**Результат:**
- Полный хеш: `aefead2207`
- Комментарий: `Update CHANGELOG.md`

---

## 2. Какому тегу соответствует коммит 85024d3?

**Как получено:**
Команда `git tag --contains 85024d3` показывает все теги, которые содержат указанный коммит (т.е. теги, которые были созданы после этого коммита или включают его). Это позволяет определить, в какой релиз вошёл данный коммит.

**Команда:**
```bash
git tag --contains 85024d3
```

**Результат:**
Коммит `85024d3` входит в следующие теги:
- `v0.12.23`
- `v0.12.24`
- `v0.12.25`
- `v0.12.26`
- `v0.12.27`
- `v0.12.28`
- `v0.12.29`
- `v0.12.30`
- `v0.12.31`

Первый тег, в который вошёл этот коммит: **v0.12.23**

---

## 3. Сколько родителей у коммита b8d720? Напишите их хеши.

**Как получено:**
Команда `git show --pretty=%P -s b8d720` выводит только родительские хеши (`%P`) указанного коммита. Флаг `-s` подавляет вывод diff. Количество выведенных хешей соответствует количеству родителей.

**Команда:**
```bash
git show --pretty=%P -s b8d720
```

**Результат:**
- Количество родителей: **2**
- Хеши родителей:
  - `56cd7859e05c36c06b56d013b55a252d0bb7e158`
  - `9ea88f22fc6269854151c571162c5bcf958bee2b`

---

## 4. Коммиты между тегами v0.12.23 и v0.12.24

**Как получено:**
Синтаксис `v0.12.23..v0.12.24` в команде `git log` означает: показать все коммиты, которые доступны из `v0.12.24`, но недоступны из `v0.12.23`. Флаг `--oneline` выводит каждый коммит в сокращённом формате (хеш + комментарий).

**Команда:**
```bash
git log --oneline v0.12.23..v0.12.24
```

**Результат:**
```bash
33ff1c03bb (tag: v0.12.24) v0.12.24
b14b74c493 [Website] vmc provider links
3f235065b9 Update CHANGELOG.md
6ae64e247b registry: Fix panic when server is unreachable
5c619ca1ba website: Remove links to the getting started guide's old location
06275647e2 Update CHANGELOG.md
d5f9411f51 command: Fix bug when using terraform login on Windows
4b6d06cc5d Update CHANGELOG.md
dd01a35078 Update CHANGELOG.md
225466bc3e Cleanup after v0.12.23 release
```

---

## 5. Коммит, в котором была создана функция func providerSource

**Как получено:**
Команда `git log -S "func providerSource"` ищет коммиты, в которых количество вхождений указанной строки изменилось (т.е. строка была добавлена или удалена). Флаг `--reverse` выводит коммиты в хронологическом порядке от старых к новым, а `| head -1` берёт первый (самый старый) коммит, где эта строка появилась.

**Команда:**
```bash
git log -S "func providerSource" --reverse --oneline | head -1
```

**Результат:**
- Хеш: `8c928e8358`
- Комментарий: `main: Consult local directories as potential mirrors of providers`

---

## 6. Коммиты, в которых изменялась функция globalPluginDirs

**Как получено:**
Команда `git log -S "globalPluginDirs" --oneline` ищет все коммиты, в которых менялось количество вхождений строки `globalPluginDirs`. Это позволяет найти все коммиты, где эта функция была добавлена, изменена или удалена.

**Команда:**
```bash
git log -S "globalPluginDirs" --oneline
```

**Результат:**
```bash
7c4aeac5f3 stacks: load credentials from config file on startup (#35952)
65c4ba7363 Remove terraform binary
125eb51dc4 Remove accidentally-committed binary
22c121df86 Bump compatibility version to 1.3.0 for terraform core release (#30988)
7c7e5d8f0a Don't show data while input if sensitive
35a058fb3d main: configure credentials from the CLI config file
c0b1761096 prevent log output during init
8364383c35 Push plugin discovery down into command package
```

---

## 7. Автор функции synchronizedWriters

**Как получено:**
Команда `git log -S "func synchronizedWriters"` ищет коммиты, где менялась эта строка. Флаг `--pretty="%an <%ae>"` форматирует вывод: только имя автора (`%an`) и email (`%ae`). `--reverse` выводит от старых к новым, а `| head -1` берёт первый коммит (где функция была создана).

**Команда:**
```bash
git log -S "func synchronizedWriters" --pretty="%an <%ae>" --reverse | head -1
```

**Результат:**
- Автор: `Martin Atkins <mart@degeneration.co.uk>`
