
## TMC

```
GET /tmc - list of tmc
  query:
    page: int,
    limit: int,
    term?: string,
    place_id?: int,
    status: string (enum)

GET /tmc/{id}

GET /tmc/category - list of tmc_category
  query:
    page: int,
    limit: int,
    term?: string

POST /tmc - create single tmc
  body: {
    status: string,
    doc_id: int,
    etc.
  }

POST /tmc/acceptance - Приемка TMC
  body: {
    doc_id: int,
    list: array list of tmc
  }

POST /tmc/category - Создание новой категории

POST /tmc/category_cheme - Создание схемы категории
  body: {
    name: string,
    column_name: string,
    type: string,
    type_sttings: JSON
  }

PATCH /tmc/{id}
  body: {
    place_id: int,
    status: string,
    name: string,
    price: int,
    serial_number: string,
    description: string,
    field: [ list of fields ],
  }
```

## place

```
GET /place - list of places
  query:
    page: int,
    limit: int,
    term: string,

GET /place/{id}

POST /place

PATCH /place/{id}
```

## worker

```
GET /worker - list of workers
  query:
    page: int,
    limit: int,
    term: string,
```

## history

```
GET /history/movement - list of movements

GET /history/movement/{tmc_id} - movements of tmc

GET /history/responsible/{place_id} - responsible change history

GET /history/tmc/{id} - history of TMC change
```

## autocomplete

```
GET /autocomplete/place
  query:
    term: string,

GET /autocomplete/place_type - Тип места / при создании нового
  query:
    term: string,

GET /autocomplete/woker - по работникам
  query:
    term: string,

GET /autocomplete/tmc_category
  query:
    term: string,

GET /autocomplete/tmc_field - поле в TMC типа tmc / при создании нового
  query:
    category: string,
    term: string,

GET /autocomplete/document
  query:
    term: string
```
