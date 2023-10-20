
#### Query para a importação de documents.json

``` shell
mongoimport --db todo_list --collection projects --file ./documents.json --jsonArray --stopOnError
```

# Queries de Inserção e Leitura

## Queries de Leitura

+ Listar todos os projetos:
    ``` shell
    db.todo_list.find({});
    ```


+ Encontrar um projeto pelo nome:
    ```shell 
    db.todo_list.find({ "name": "Project A" });
    ```


+ Listar todas as tarefas de um projeto:
    ``` shell
    db.todo_list.aggregate([
    { $match: { "name": "Project A" } },
    { $unwind: "$tasks" },
    { $replaceRoot: { newRoot: "$tasks" } }
    ]);
    ```


+ Encontrar um usuário pelo nome:
    ``` shell
    db.todo_list.find({ "createdBy.name": "Admin" });
    ```


+ Listar todas as tarefas de um usuário:
    ``` shell
    db.todo_list.find({ "tasks.user.name": "John Doe" });
    ```


+ Listar todas as tarefas com status "To-Do" (a fazer) em um projeto:
    ``` shell
    db.todo_list.find({ "name": "Project A", "tasks.status": "Pending" });
    ```


+ Listar todas as tarefas com status "To-Do" (a fazer) de um usuário:
    ``` shell
    db.todo_list.find({ "tasks.user.name": "John Doe", "tasks.status": "Pending" });
    ```


+ Listar todas as tarefas com prazo de entrega vencido:
    ``` shell
    db.todo_list.find({ "tasks.dueDate": { $lt: new Date() }, "tasks.status": { $ne: "Completed" } });
    ```


+ Encontrar todos os projetos criados por um usuário:
    ``` shell
    db.todo_list.find({ "createdBy.name": "Admin" });
    ```


+ Listar todas as tarefas de um projeto ordenadas por prioridade:
    ``` shell
    db.todo_list.find({ "name": "Project A" }, { "tasks": { $elemMatch: { $exists: true } } }).sort({ "tasks.priority": -1 });
    ```


+ Encontrar todas as tarefas de um usuário em andamento:
    ```shell
    db.todo_list.find({ "tasks.user.name": "John Doe", "tasks.status": "In Progress" });
    ```


+ Listar todos os projetos criados em uma data específica:
    ```shell
    db.todo_list.find({ "createdAt": "01/10/2023" });
    ```

+ Listar todas as tarefas de um projeto criadas entre duas datas:
    ```shell
    db.todo_list.find({
    "name": "Project A",
    "tasks.createdAt": { $gte: "01/10/2023", $lte: "31/12/2023" }
    });
    ```


+ Encontrar todos os usuários associados a um projeto:
    ```shell
    db.todo_list.aggregate([
    { $match: { "name": "Project A" } },
    { $unwind: "$tasks" },
    { $replaceRoot: { newRoot: "$tasks.user" } },
    { $group: { _id: "$name", users: { $addToSet: "$$ROOT" } } }
    ]);
    ```


+ Listar todas as tarefas de um projeto com descrição contendo uma palavra-chave:
    ```shell
    db.todo_list.find({
    "name": "Project A",
    "tasks.description": { $regex: /initial project planning/i }
    });
    ```
