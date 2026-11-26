# Сутності та атрибути

| Сутність             | Атрибути               |
| -------------------- | ----------------------------------------------- |  
| EMPLOYEE | id, first_name, last_name, email, phone |
| STORE | id, name, address |
| ROLE | id, name |
| SHIFT | id, start_time, end_time |
| SHIFT_ASSIGNMENT | id, assigned_at, status |
| SWAP_REQUEST | id, created_at, reason, status, decided_at |
| UNAVAILABILITY | id, start_time, end_time |

# Типи даних

| Атрибути             | Тип        |
| -------------------- | ---------- |
| id                 | int      |
| Імена, адреси, назви | string  |
| Телефон та email     | string   |
| Дата й час           | datetime |
| Причина заявки       | string   |
| Статус               | enum    |
| decided_at               | datetime, необовязковий  |

# Зв'язки між сутностями

| Сутність A       | Сутність B                | Кількість B для одного A | Кількість A для одного B |
| ---------------- | ------------------------- | ------------------------ | ------------------------ |
| EMPLOYEE         | STORE                     | 0..N                     | 0..N                     |
| EMPLOYEE         | ROLE                      | 0..N                     | 0..N                     |
| STORE            | SHIFT                     | 0..N                     | 1                        |
| EMPLOYEE         | SHIFT_ASSIGNMENT          | 0..N                     | 1                        |
| SHIFT            | SHIFT_ASSIGNMENT          | 0..N                     | 1                        |
| EMPLOYEE         | UNAVAILABILITY            | 0..N                     | 1                        |
| SHIFT_ASSIGNMENT | SWAP_REQUEST (offered)    | 0..N                     | 1                        |
| SHIFT_ASSIGNMENT | SWAP_REQUEST (requested)  | 0..N                     | 1                        |
| EMPLOYEE         | SWAP_REQUEST (decided_by) | 0..N                     | 0..1                     |

# Критерії прийняття

| Критерій | Необхідне уточнення                                                                                          |
| -------- | ------------------------------------------------------------------------------------------------------------ |
| AC-01    | Рівно сім визначених сутностей з узгодженими атрибутами                                                    |
| AC-02    | Кардинальності відповідають уточненій таблиці зв'язків                                                   |
| AC-03    | EMPLOYEE–ROLE та EMPLOYEE–STORE є прямими M:N                                                               |
| AC-04    | SHIFT_ASSIGNMENT містить власні атрибути `assigned_at` та `status`                                    |
| AC-05    | Відсутні списки значень, часткові й транзитивні залежності неключових атрибутів                           |
| AC-06    | Усі ідентифікатори мають тип `int`, часові поля — `datetime`                                              |
| AC-07    | Використано Mermaid `erDiagram`                                                                         |
| AC-08    | SVG згенеровано безпосередньо з декларативної моделі                                                       |
| AC-09    | Відсутні SQL, ORM та фізична схема БД                                                                  |
| AC-10    | Заявка має два окремі зв'язки з призначеннями та необов'язковий зв'язок із менеджером, який прийняв рішення |
| AC-11    | UNAVAILABILITY описує виключно періоди недоступності                                                     |
| AC-12    | Ролі працівника не залежать від конкретного магазину                                                        |