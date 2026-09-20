# Лабораторная работа 2 — ветвление и слияние Git

Проект выполнен в общем репозитории `PI`. Основная ветвь — `main`, согласно уточнению к заданию. Она используется во всех местах, где в исходном условии написано `master`.

Репозиторий: [annatemeshova/PI](https://github.com/annatemeshova/PI).

Отчет: [Отчет ЛР2 Git.docx](../Отчеты/ЛР2/Отчет%20ЛР2%20Git.docx).

## Материалы

- `project.txt`, `plan.txt`, `settings.txt` — три исходных файла, каждый начинался с трех строк.
- `feature.txt` — результат объединения двух фиксаций через squash.
- `cherry-pick.txt` — файл, перенесенный отдельной фиксацией.
- `screenshots/` — 19 PNG: 17 снимков сохраненных протоколов в оформлении macOS Terminal и два настоящих снимка окна KDiff3 до и после разрешения конфликта.
- `protocol/` — команды, фактический вывод, время выполнения и коды завершения. HTML — страницы протокола, снимки которых вставлены в отчет; TXT и JSON содержат неизмененные исходные данные. Для читаемости в некоторых иллюстрациях показаны фрагменты: пропуски отмечены многоточием.
- `protocol/screenshot-manifest.json` — соответствие иллюстраций записям исходного протокола. Оформление повторяет предоставленный образец Terminal; иллюстрации протоколов не являются снимками живого окна Terminal.
- `protocol/commits.json` — полные идентификаторы ключевых фиксаций.
- `Project2-history.bundle` — проверенная резервная копия истории на момент завершения пункта 14, до добавления отчета и иллюстраций.

В пункте 14 инструмент KDiff3 сопоставил базу `mode=base`, локальную версию `mode=stable` и входящую `mode=feature`. Через меню **Merge → Choose B for All Unsolved Conflicts** выбран локальный вариант `mode=stable`, затем файл сохранен. Итоговая фиксация слияния — `ca3eadb`, родители `7b46a12` и `8fce157`. Ее дерево совпадает с первым родителем, поскольку единственный конфликт разрешен в пользу `main`; при этом граф правильно объединяет обе ветви.

Ветка `br1` после пункта 14 сохранена: задание не требует удалять ее после последнего слияния. Отчет и доказательства добавлены отдельной служебной фиксацией после учебных операций.

## Проверка для защиты

Команды выполняются из каталога `PI` или `Project2`:

```sh
git log --graph --oneline --decorate main br1
git show --no-patch --format=fuller refs/lab2/merge-br1-br2
git log --graph --oneline refs/lab2/br2-before-rebase
git log --graph --oneline refs/lab2/br2-after-rebase
git show --no-patch --format='%h %p %s' refs/lab2/squash
git show --no-patch --format=full refs/lab2/cherry-result
git show --no-patch --format='%h %p %s' refs/lab2/final
git status --short --branch
```

Контрольные ссылки `refs/lab2/*` сохраняют историю, которую обычный rebase и удаление ветвей сделали бы недоступной после очистки Git. Это не дополнительные рабочие ветви. Все операции лабораторной выполнены с ветвями `main`, `br1`, `fix1` и `br2`.

Для отдельного восстановления истории из bundle:

```sh
git clone -b main Project2-history.bundle Project2-check
git -C Project2-check fetch origin 'refs/lab2/*:refs/lab2/*'
```

KDiff3 1.12.6 расположен в `/Users/fedos-mak/Documents/lr-Guz/.tools/kdiff3.app`. Путь к нему настроен локально в репозитории. Дистрибутив получен с официального сайта KDE: https://download.kde.org/stable/kdiff3/.
