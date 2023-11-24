## Общие пожелания

- Результатом выполнения задания является ссылка на приватный репозиторий GitHub, GitLab или Bitbucket.
- Мы будем оценивать не только работоспособность кода, но также его структуру, качество, надежность и гибкость.
- Также следует написать модульные тесты.

## Задание

Дан демонстрационный сервис, который по GET-запросу на /posts/id отдает комментарий в нотации JSON по его числовому идентификатору id.

Например, 
```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```
Пусть есть дерево идентификаторов в нотации JSON, структуру которого можно понять из следующего примера:

```json
{
  "id": 1,
  "replies": [
    {
      "id": 2,
      "replies": []
    },
    {
      "id": 3,
      "replies": [
        {
          "id": 4,
          "replies": []
        },
        {
          "id": 5,
          "replies": []
        }
      ]
    }
  ]
}
```

Необходимо написать утилиту командной строки (CLI), которая принимает на стандартный поток ввода такое дерево идентификаторов, после чего печатает на стандартный поток вывода такое же дерево, в котором также присутствуют тела сообщений соответствующих комментариев, например:

```json
{
  "id": 1,
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita...",
  "replies": [
    {
      "id": 2,
      "body": "est rerum tempore vitae...",
      "replies": []
    },
    {
      "id": 3,
      "body": "et iusto sed quo iure...",
      "replies": [
        {
          "id": 4,
          "body": "ullam et saepe reiciendis voluptatem adipisci...",
          "replies": []
        },
        {
          "id": 5,
          "body": "repudiandae veniam quaerat sunt sed...",
          "replies": []
        }
      ]
    }
  ]
}
```

Важно, что мы хотим загружать все комментарии параллельно, а не последовательно, поскольку сервис возвращает комментарии по одному. Иными словами, если не делать никаких предположений о возможном распределении задержек ответа от сервиса, а также пренебречь процессорным временем и затратами на ввод-вывод, то в идеальном случае время работы программы должно быть приближено к определяемому формулой $\max{t_i}$, а не к $\sum{t_i}$ , где  ${t_i}$— задержка сервиса при ответе на ${i}$-ый запрос.
