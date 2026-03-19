> REST provides a set of architectural constraints that, when applied as a whole, emphasizes scalability of component interactions, generality of interfaces, independent deployment of components, and intermediary components to reduce interaction latency, enforce security, and encapsulate legacy systems.

### Проблема получения нескольких ресурсов через один запрос
В терминологии REST ресурс обычно относится к определённой бизнес-сущности. Поэтому если клиенту необходимо получить данные о связанных сущностях, он вынужден использовать несколько сетевых запросов. Для решения этой проблемы можно на стороне сервера при формировании ответа дополнительно включать информацию о связанных объектах. Глубину передаваемого графа объектов можно контролировать через входные параметры запроса:
```
GET /orders/order-id-1345?expand=consumer
```
В более сложных сценариях используют [[GraphQL]]
### Проблема выбора HTTP глагола для операции
Если для операции над ресурсом не очевидно, какой метод для неё нужно использовать (обычно сложности возникают в выборе между POST, PUT или PATCH), то можно выделить для такой операции отдельный ресурс:
```
POST /orders/{orderId}/cancel
POST /orders/{orderId}/revise
```