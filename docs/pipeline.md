# Воронка

## Настройка

```php
$pipeline = new \linkprofit\AmoCRM\entities\Pipeline();
$pipeline->name = 'Воронка';
$pipeline->sort = 2;
$pipeline->is_main = 'on';
```

создаем `Status` для `Pipeline`
```php
$status = new \linkprofit\AmoCRM\entities\Status();
$status->name = 'Статус';
$status->sort = 1;
$status->color = '#fffeb2';
```
Добавляем `Status` в `Pipeline`, их может быть несколько одновременно
```php
$pipeline->addStatus($status);
```

## Использование
Инициализируйте сервис с объектом [linkprofit\AmoCRM\RequestHandler](/docs/request.md) и добавьте объект класса `linkprofit\AmoCRM\entities\Pipeline` методом `add()`.
Вы можете добавить несколько сущностей для множественного добавления/обновления

```php
$pipelineService = new \linkprofit\AmoCRM\services\PipelineService($request);
$pipelineService->add($pipeline);
```

Метод `save()` вернет `response` сервера в случае успеха. В случае неудачи метод вернет `false`.

Если вам необходимо обработать ответ, вы можете воспользоваться методом `parseResponseToEntities()`, который вернет массив добавленных объектов `linkprofit\AmoCRM\entities\Pipeline` с инициализированным свойством `id`, который вернулся ответом сервера на наш запрос.

### Получение списка существующих элементов
Просто вызовите метод `getList()` у сервиса, в ответ придет массив объектов класса `linkprofit\AmoCRM\entities\Pipeline`. Ограничения на один запрос 500 элементов
```php
$pipelines = $service->getList(); //Вернет массив всех элементов (не более 500)
```

Отельно элемент можно получить по его id, в ответ придет массив с единственным элементом `linkprofit\AmoCRM\entities\Pipeline`
```php
$elementId = 1232;
$pipeline = $service->setId($elementId)->getList();