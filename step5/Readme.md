# Operações de Update

## Alterar o usuário responsável por uma tarefa:
```shell
db.projects.update(
   { "tasks.user.name": "Owen Brown" },
   { $set: { "tasks.$.user.name": "Novo Responsável" } },
   { multi: true }
)
```

Esta query altera o nome do usuário responsável pela tarefa de "Owen Brown" para "Novo Responsável".

## Dilatar o prazo de entrega da tarefa:
``` shell
db.projects.update(
   { "tasks.dueDate": "2023-05-10" },
   { $set: { "tasks.$.dueDate": "2023-06-30" } },
   { multi: true }
)
```

Esta query altera a data de vencimento das tarefas com a data "2023-05-10" para "2023-06-30".

## Mudar o status de "In Progress" para "Complete":

``` shell
db.projects.update(
   { "tasks.status": "In Progress" },
   { $set: { "tasks.$.status": "Complete" } },
   { multi: true }
)
```

Esta query muda o status das tarefas em andamento para "Complete".

## Adicionar uma nova tarefa a um projeto específico:

``` shell
db.projects.update(
   { "name": "Project U" },
   { $push: { "tasks": { 
      "title": "Nova Tarefa",
      "description": "Descrição da Nova Tarefa",
      "status": "Pending",
      "user": {
         "name": "Novo Usuário",
         "role": "Novo Cargo"
      },
      "dueDate": "2023-07-31",
      "priority": "Medium"
   } } }
)
``` 

Esta query adiciona uma nova tarefa ao projeto com o nome "Project U".

## Atualizar a data de criação de um projeto específico:

``` shell
db.projects.update(
   { "name": "Project V" },
   { $set: { "createdAt": "2023-01-15" } }
)
``` 
Esta query atualiza a data de criação do projeto com o nome "Project V" para "2023-01-15".