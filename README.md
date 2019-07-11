# Bitrix Elasticsearch Indexer

[![pipeline status](https://gitlab.com/sheerockoff/bitrix-elastic-indexer/badges/master/pipeline.svg)](https://gitlab.com/sheerockoff/bitrix-elastic-indexer/pipelines)
[![coverage report](https://gitlab.com/sheerockoff/bitrix-elastic-indexer/badges/master/coverage.svg)](https://gitlab.com/sheerockoff/bitrix-elastic-indexer/-/jobs)

Хелпер для индексации данных инфоблока Bitrix в Elasticsearch.

## Быстрый старт

Подключаем зависимости, создаём клиент Elasticsearch, создаём экземпляр `Indexer`.

```php
<?php

use Elasticsearch\ClientBuilder;
use Sheerockoff\BitrixElastic\Indexer;

require 'vendor/autoload.php';

$elastic = ClientBuilder::create()->setHosts(['http://elasticsearch:9200'])->build();
$indexer = new Indexer($elastic);
```

Получаем карту индекса для инфоблока.

```php
$mapping = $indexer->getInfoBlockMapping($iBlockId);
```

Получаем сырые данные индекса для элемента.

```php
/** @var _CIBElement $element */
$rawData = $indexer->getElementIndexData($element);
```

Нормализуем сырые данные индекса в соответствии с картой индекса.

```php
$data = $indexer->normalizeData($mapping, $rawData);
```