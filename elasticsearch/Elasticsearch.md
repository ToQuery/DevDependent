
显示所有索引

GET /_cat/indices?v&pretty

查看索引event2021-10-09的所有数据

GET /event2021-10-09/_search

POST /_sql?format=txt&pretty
{
  "query":"select * from \"event2021-10-09\" group by deviceIp"
}

POST /_xpack/sql?format=txt&pretty
{
  "query":"select * from \"event2021-10-09\" group by deviceIp"
}

POST /_sql/translate?format=json&pretty
{
  "query":"select * from \"event2021-10-09\" group by deviceIp"
}
