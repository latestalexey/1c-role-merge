# Объединение ролей в 1С

## Описание

Идея проекта: При использовании RLS часто у заказчика появляется возражение о скорости работы пользователей ограниченных по правам. Типичным решением такой ситуации является - анализ прав и их упрощение, возможно даже до уровня - роль для каждого пользователя. Такая потребность натолкнула на мысль об автоматизации труда программиста.

## Использование

1. В конфигурации создаем роль которая будет хранить результат объединения прав нескольких ролей
2. Выгружаем конфигурацию в файлы
3. Запускаем 1С предприятие в режиме управляемое приложение
4. Открываем обработку "1c-role-merge.epf"
5. В открывшемся окне выбираем путь до "Файл роли приемника" (Созданная нами роль, для версии платформы 8.3.16 пример пути ".\src\Roles\РольПриемник\Ext\Rights.xml")
6. В табличной части указываем пути до файлов прав ролей которые требуется объединить
7. Выполняем команду "Объединить"
8. Загружаем конфигурацию из файлов

## Особенности

В версии платформы 8.3.15 при выгрузке не верно формируется пространство имен. Чтобы устранить проблему вставьте, до объединения, вручную верное пространства имен в файл роли приемника.

НЕ ВЕРНО:

```xml
<Rights xmlns="http://v8.1c.ru/8.2/roles" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" version="2.9">
```

ВЕРНО:

```xml
<Rights xmlns="http://v8.1c.ru/8.2/roles" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="Rights" version="2.9">
```

[Лицензия](LICENSE.md)

[Договоренности о доработках](CONTRIBUTING.md)

[Проект внешних обработок и отчетов EDT](src/1C-EDT/src)

[За основу взята обработка с портала Инфостарт](https://infostart.ru/public/487724/)

### TODO

1. Сделать на OScript, чтобы не быть привязанным к 1С предприятию
2. Добавить в обработку визуализацию прав, чтобы при пересечении ограничений на запись можно было интерактивно выбирать нужные нам настройки
