# Руководство по системному администрированию

В данном документе описаны сценарии администрирования программного компонента **Deploy tools** 
(`CDJE`).

## Сценарии администрирования
[Subscribe to our newsletter](#){ .md-button }

### Термины и определения

##### Запуск Service job

Первым шагом выполните реконфигурацию Service job (Запуск Jenkins job с пустыми параметрами).

Для миграции конфигураций при помощи Service job произведите ее запуск со следующими параметрами:
```yaml
# Обновляемый компонент
ARTIFACT_TYPE: "COMMON"
# Версия, на которую будет произведено обновление
ARTIFACT_VERSION: <Версия выпущенного ранее дистрибутива common>
# Выбор этапа (stage – определяющего какую часть компонента требуется обновить)
PARAMETERS:
  - MIGRATION_CONFIGURATION
```

### Работа с файлом subsystems.json

После обновления Pipeline (см. [**Руководство по установке**](../../installation-guide/md/index.md) → подпункт *Проведение последовательной миграции subsystems*) через Service job в репозитории **common** создается/обновляется основной конфигурационный файл для устанавливаемых конфигураций функциональных приложений – ***subsystems.json***

Пример заполнения файла *subsystems.json*:


### Организация секций стенда в environment.json и секций подсистем в subsystems.json

Определение секции стенда или подсистемы в файлах environment.json и subsystems.json 
позволяет задать значения параметров, специфичных для конкретного стенда или подсистемы. 
При этом, если параметр уже определен в секции стенда или подсистемы, 
то его значение не будет перезаписано значением из секции по умолчанию.

#### Структура файла environment.json

Файл environment.json содержит информацию о различных стендах. 
Разберем как работает переопределение параметров на простом и наглядном примере:

```json
{
   "__default": {
      "param1": "value1",
      "param2": "value3"
   },
   "stand1": {
      "param1": "value2"
   },
   "stand2": {
      "param2": "value4"
   },
   "standN": {
      "param3": "value5"
   }
}
```

Секция **__default** представляет собой секцию по умолчанию, 
в которой определены значения параметров **param1** и **param2**. 
Значения параметров в секции по умолчанию будут использоваться для стендов, 
у которых эти параметры не определены явно.

Каждая последующая секция (например, **stand1**, **stand2**, **standN**) 
представляет отдельный стенд и может содержать переопределение значений параметров либо добавление 
новых, специфичных только для этого стенда параметров. 
Например, в секции **stand1** значение параметра **param1** переопределено и равно **value2**, 
а параметр **param2** в секции отсутствует, поэтому он наследуется из секции по умолчанию.

#### Преобразование значений

После преобразования, значения параметров в секциях стенда будут перезаписаны 
значениями из секции по умолчанию, если они не определены явно. 
Однако, если параметр уже определен в секции стенда, то его значение останется неизменным.

Пример результата преобразования:

```json
{
   "stand1": {
      "param1": "value2",
      "param2": "value3"
   },
   "stand2": {
      "param1": "value1",
      "param2": "value4"
   },
   "standN": {
      "param1": "value1",
      "param2": "value3",
      "param3": "value5"
   }
}
```

В данном примере, значения параметров **param1** в секции **stand1** остался неизменным, а **param2** был добавлен из секции по умолчанию.<br>
В секции **stand2** ситуация аналогичная секции **stand1**, но из секции по умолчанию добавлен уже **param1**.<br>
В секции **standN** параметры **param1** и **param2** были унаследованы из секции по умолчанию, а параметр **param3** остался со значением **value5**.

#### Переопределение параметров подсистем в subsystems.json

Логика переопределения параметров подсистем в subsystems.json 
аналогична логике переопределения параметров стендов в environment.json.

## События системного журнала

У программного компонента Deploy tools отсутствует встроенный системный журнал. События каждого запуска Deploy tools логируются средствами сервиса Jenkins и сохраняются в его логах.

События аудита программного компонента Deploy tools не генерируются.

## События мониторинга

У программного компонента **Deploy tools** отсутствуют события мониторинга.

## Часто встречающиеся проблемы и пути их устранения

