https://github.com/simdjson/simdjson?tab=readme-ov-file
Бібліотека simdjson використовує загальнодоступні SIMD-інструкції та алгоритми для розбору JSON у 4 рази швидше, ніж RapidJSON, і в 25 разів швидше, ніж JSON for Modern C++.

Особливості simdjson: 
 - мініфікація JSON зі швидкістю 6 ГБ/с, перевірка UTF-8 зі швидкістю 13 ГБ/с, NDJSON зі швидкістю 3,5 ГБ/с
 - прості у використанні та ретельно документовані API
 - повна валідація JSON і UTF-8, парсинг відбувається без втрат 
 - сам вибирає відповідний парсер, не потрібно налаштовувати

simdjson використовується у Facebook/Meta, у ClickHouse, WatermelonDB, Apache Doris, Milvus, StarRocks