---
## Author
author:
  name: Иванова Анастасия Сергеевна
  degrees: DSc
  orcid: 0000-0002-0877-7063
  email: 1132250427@rudn.ru
  affiliation:
    - name: Российский университет дружбы народов
      country: Российская Федерация
      postal-code: 117198
      city: Москва
      address: ул. Миклухо-Маклая, д. 6

## Title
title: "Отчет по лабораторной работе №4"
subtitle: "по курсу: Архитектура компьютера и операционные системы"
license: "CC BY"
---

# Цель работы

Получение навыков правильной работы с репозиториями git.

# Выполнение лабораторной работы

([рис. @fig-001]):

![Переход в каталог](image/1.png){#fig-001 width=70%}

## 1. Установка программного обеспечения

Сначала мы установили все необходимые инструменты. Для этого подключили репозиторий Copr и установили git-flow. Затем установили Node.js и pnpm, после чего выполнили настройку pnpm и обновили переменные окружения.

sudo dnf copr enable elegos/gitflow
sudo dnf install gitflow
sudo dnf install nodejs
sudo dnf install pnpm
pnpm setup
source ~/.bashrc

##  2. Установка инструментов для работы с коммитами

Далее мы установили commitizen для форматирования коммитов и standard-changelog для автоматической генерации журнала изменений.

pnpm add -g commitizen
pnpm add -g standard-changelog

## 3. Создание репозитория на GitHub

После этого через веб-интерфейс GitHub мы создали новый пустой репозиторий с названием git-extended.

## 4. Инициализация локального репозитория

Затем мы перешли в домашний каталог, создали папку git-extended и инициализировали в ней git-репозиторий. После создания файла README.md мы добавили его в индекс и сделали первый коммит. Наконец, связали локальный репозиторий с удалённым и отправили изменения на GitHub.

cd ~/git-extended
git init
echo "# git-extended" > README.md
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:asivanova1/git-extended.git
git push -u origin master

## 5. Настройка конфигурации для общепринятых коммитов

Далее мы выполнили инициализацию Node.js-пакета командой pnpm init и отредактировали файл package.json, добавив в него конфигурацию для commitizen.

## 6. Выполнение первого коммита через commitizen

После этого мы добавили все файлы в индекс и выполнили коммит с помощью git cz, выбрав соответствующий тип изменения и описав его. Затем отправили изменения на GitHub.

git add .
git cz
git push

## 7. Инициализация git-flow

Теперь мы инициализировали git-flow в нашем репозитории. В процессе настройки указали префикс для версионных ярлыков как v.

git flow init

## 8. Настройка ветки develop

Затем мы отправили все ветки на GitHub и установили вышестоящую ветку для локальной ветки develop, связав её с удалённой.

git push --all
git branch --set-upstream-to=origin/develop develop

## 9. Создание первого релиза (версия 1.0.0)

Дальше мы приступили к созданию релиза. Создали релизную ветку 1.0.0, сгенерировали файл CHANGELOG.md с описанием изменений и добавили его в индекс. После коммита завершили релиз, объединив ветки и создав тег. В конце отправили все изменения и теги на GitHub, а также создали релиз через GitHub CLI.

git flow release start 1.0.0
standard-changelog --first-release
git add CHANGELOG.md
git commit -am 'chore(site): add changelog'
git flow release finish 1.0.0
git push --all
git push --tags
gh release create v1.0.0 -F CHANGELOG.md

## 10. Работа с функциональной веткой

Затем мы создали функциональную ветку для разработки новой возможности. После завершения работы объединили её с веткой develop и удалили.

git flow feature start feature_branch
git flow feature finish feature_branch

## 11. Создание второго релиза (версия 1.2.3)

Наконец, мы создали ещё один релиз с обновлённой версией. Для этого создали релизную ветку 1.2.3, обновили номер версии в файле package.json и заново сгенерировали журнал изменений. Затем добавили обновлённый CHANGELOG.md в индекс и выполнили коммит. После завершения релиза отправили все изменения и теги на GitHub и создали новый релиз.

git flow release start 1.2.3
standard-changelog
git add CHANGELOG.md
git commit -am 'chore(site): update changelog'
git flow release finish 1.2.3
git push --all
git push --tags
gh release create v1.2.3 -F CHANGELOG.md


# Вывод

Мы получили навыков правильной работы с репозиториями git.

::: {#refs}
:::
