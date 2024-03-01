# API de un sistema de reserva de butacas de cine

En este ejercicio vamos a diseñar la API REST para el cine en el que venimos trabajando en los ejercicios de los anteriores temas.

Las operaciones que la API debe soportar son las siguientes:
- Crear, eliminar y modificar películas.
- Crear, eliminar y modificar (parcialmente) salas.
- Crear, eliminar y modificar (parcialmente) usuarios.
- Crear una reserva para un usuario en una sala.
- Cancelar una reserva para un usuario en una sala.
- Modificar una reserva para un usuario en una sala.
- Registrar un pago de una reserva.

## Propuesta

**Recursos identificados:**

- Pelicula (movies): Representa el catalogo de peliculas disponibles en el cine
- Sala (screens): Representa las salas presentes en el cinema
- Usuario (clients): Representan los clientes del cinema
- Reserva (bookings): Representan las reservas que los clientes hacen en el cinema
- Pago (payments): Representan los pagos de las reservas

| Método HTTP | URI            | Query Params | Cuerpo de la Petición                                                                                                                                                                   | Cuerpo de la Respuesta                                                                                                                                                                   | Códigos de Respuesta                                                       |
|-------------|----------------|-----|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| POST        | /movies        | N/A | `{"name": "El niño y la garza", "director": ["Hayao Miyazaki"], "genre": ["Anime"], "rating": "PG-13", "synopsis": "....", "availability": {"from": "01-01-2024", "until": "31-12-2024"}}` | `{"id": "1", "name": "El niño y la garza", "director": ["Hayao Miyazaki"], "genre": ["Anime"], "rating": "PG-13", "synopsis": "....", "availability": {"from": "01-01-2024", "until": "31-12-2024"}}` | 201 Created<br/>400 Bad request<br/>500 Internal Server Error              |
| PATCH       | /movies/{id}   |N/A| `{"availability": {"from": "01-01-2024", "until": "01-02-2024"}`                                                                                                                        | `{"id": "1", "name": "El niño y la garza", "director": ["Hayao Miyazaki"], "genre": ["Anime"], "rating": "PG-13", "synopsis": "....", "availability": {"from": "01-01-2024", "until": "01-02-2024"}}` | 200 Ok<br/>400 Bad request<br/>404 Not found<br/>500 Internal Server Error |
| DELETE      | /movies/{id}   |N/A| N/A                                                                                                                                                                                     | N/A                                                                                                                                                                                      | 200 Ok<br/>404 Not founf<br/>500 Internal Server Error                     |
| POST        | /screens       | N/A | `{"id": 1, "seats": 40}`                                                                                                                                                                | `{"id": 1, "seats": 40}`                                                                                                                                                                 | 201 Created<br/>400 Bad request<br/>500 Internal Server Error              |
| PATCH       | /screens/{id}  | N/A | `{"seats": "50"}`                                                                                                                                                                       | `{"id": 2, "seats": 50}`                                                                                                                                                                 | 200 OK<br/>404 Not found<br/>400 Bad request<br/>500 Internal Server Error |
| DELETE      | /screens/{id}  | N/A | N/A                                                                                                                                                                                     | N/A                                                                                                                                                                                      | 200 OK<br/>404 Not found<br/>400 Bad request<br/>500 Internal Server Error |
| POST        | /users         |N/A| `{"name":"Julian Avellaneda","phone":"1234567890","email":"uncorreo@mail.com"}`                                                                                                         | `{"id": "1", "name":"Julian Avellaneda","phone":"1234567890","email":"uncorreo@mail.com"}`                                                                                               | 201 Created<br/>400 Bad request<br/>500 Internal Server Error              |
| PATCH       | /users/{id}    |N/A| `{"phone":"987654321"}`                                                                                                                                                                 | `{"id": "1", "name":"Julian Avellaneda","phone":"987654321","email":"uncorreo@mail.com"}`                                                                                                | 200 OK<br/>404 Not found<br/>400 Bad request<br/>500 Internal Server Error |
| DELETE      | /users/{id}    |N/A| N/A                                                                                                                                                                                     | N/A                                                                                                                                                                                      | 200 Ok<br/>404 Not found<br/>400 Bad request<br/>500 Internal Server Error |
| POST        | /bookings      |N/A| `{"user":1,"movie":1,"screen":1,"price":10000}`                                                                                                                                         | `{"id":1, user":1,"movie":1,"screen":1,"price":10000}`                                                                                                                                   | 201 Created<br/>400 Bad request<br/>500 Internal Server Error              |
| PATCH       | /bookings/{id} |N/A| `{"price":20000}`                                                                                                                                                                       | `{"id":1, user":1,"movie":1,"screen":1,"price":20000}`                                                                                                                                   | 200 OK<br/>400 Bad request<br/>404 Not found<br/>500 Internal Server Error |
| DELETE      | /bookings/{id} |N/A| N/A                                                                                                                                                                                     | N/A                                                                                                                                                                                      | 200 OK<br/>400 Bad request<br/>404 Not found<br/>500 Internal Server Error |
| POST        | /payments      |N/A| `{"book":1,"method":"CASH","amount":1000}`                                                                                                                                                                                        | `{"id": 1, "book":1,"method":"CASH","amount":1000, "status": "PROCESSED"}`                                                                | 200 OK<br/>400 Bad request<br/>404 Not found<br/>500 Internal Server Error |
