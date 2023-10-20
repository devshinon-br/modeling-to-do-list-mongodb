
## Queries de Leitura

+ Listar todos os projetos:
    ``` shell
    db.projects.find({});
    ```

    + Resultados:
    ``` shell
    [
    {
        _id: ObjectId("6531d5884f303a7b6a920477"),
        name: 'Project H',
        startDate: '2023-05-03',
        endDate: '2023-12-04',
        tasks: [
        {
            title: 'Task 1',
            description: 'Develop project timeline',
            status: 'In Progress',
            user: { name: 'Daniel Garcia', role: 'Project Scheduler' },
            dueDate: '2023-11-04',
            priority: 'High'
        },
        {
            title: 'Task 2',
            description: 'Coordinate team meetings',
            status: 'Pending',
            user: { name: 'Mia Rodriguez', role: 'Team Coordinator' },
            dueDate: '2023-10-04',
            priority: 'Low'
        }
        ],
        createdBy: { name: 'Admin', role: 'Administrator' },
        createdAt: '2023-01-02',
        updatedAt: '2023-10-02'
    },
    {
        _id: ObjectId("6531d5884f303a7b6a920478"),
        name: 'Project C',
        startDate: '2023-02-04',
        endDate: '2023-11-06',
        tasks: [
        {
            title: 'Task 1',
            description: 'Define project scope',
            status: 'Completed',
            user: { name: 'Eva Davis', role: 'Project Analyst' },
            dueDate: '2023-10-05',
            priority: 'High'
        },
        {
            title: 'Task 2',
            description: 'Conduct team training',
            status: 'Pending',
            user: { name: 'Tom Robinson', role: 'Training Specialist' },
            dueDate: '2023-10-05',
            priority: 'Medium'
        }
        ],
        createdBy: { name: 'Admin', role: 'Administrator' },
        createdAt: '2023-01-03',
        updatedAt: '2023-05-03'
    }, 
    ..... #it have more results but should be bad to visualize
    ``` 


+ Encontrar um projeto pelo nome:
    ```shell 
    db.projects.find({ "name": "Project A" });
    ```
    
    + Resultados:
    ``` shell
    [
        {
            _id: ObjectId("6531d5884f303a7b6a920493"),
            name: 'Project A',
            startDate: '2023-11-11',
            endDate: '2023-12-12',
            tasks: [
            {
                title: 'Task 1',
                description: 'Complete initial project planning',
                status: 'In Progress',
                user: { name: 'John Doe', role: 'Project Manager' },
                dueDate: '2023-10-11',
                priority: 'High'
            },
            {
                title: 'Task 2',
                description: 'Develop prototype',
                status: 'Pending',
                user: { name: 'Jane Smith', role: 'Developer' },
                dueDate: '2023-10-12',
                priority: 'Medium'
            }
            ],
            createdBy: { name: 'Admin', role: 'Administrator' },
            createdAt: '2023-01-10',
            updatedAt: '2023-05-10'
        }
    ]
    ```


+ Listar todas as tarefas de um projeto:
    ``` shell
    db.projects.aggregate([
    { $match: { "name": "Project A" } },
    { $unwind: "$tasks" },
    { $replaceRoot: { newRoot: "$tasks" } }
    ]);
    ```

    + Resultados:
    ``` shell
        [
            {
                title: 'Task 1',
                description: 'Complete initial project planning',
                status: 'In Progress',
                user: { name: 'John Doe', role: 'Project Manager' },
                dueDate: '2023-10-11',
                priority: 'High'
            },
            {
                title: 'Task 2',
                description: 'Develop prototype',
                status: 'Pending',
                user: { name: 'Jane Smith', role: 'Developer' },
                dueDate: '2023-10-12',
                priority: 'Medium'
            }
        ]
    ```


+ Encontrar projetos pelo nome de quem criou o projeto:
    ``` shell
    db.projects.find({ "createdBy.name": "Admin" });
    ```

    + Resultados:
    ``` shell
    [
    {
        _id: ObjectId("6531d5884f303a7b6a920477"),
        name: 'Project H',
        startDate: '2023-05-03',
        endDate: '2023-12-04',
        tasks: [
        {
            title: 'Task 1',
            description: 'Develop project timeline',
            status: 'In Progress',
            user: { name: 'Daniel Garcia', role: 'Project Scheduler' },
            dueDate: '2023-11-04',
            priority: 'High'
        },
        {
            title: 'Task 2',
            description: 'Coordinate team meetings',
            status: 'Pending',
            user: { name: 'Mia Rodriguez', role: 'Team Coordinator' },
            dueDate: '2023-10-04',
            priority: 'Low'
        }
        ],
        createdBy: { name: 'Admin', role: 'Administrator' },
        createdAt: '2023-01-02',
        updatedAt: '2023-10-02'
    },
    {
        _id: ObjectId("6531d5884f303a7b6a920478"),
        name: 'Project C',
        startDate: '2023-02-04',
        endDate: '2023-11-06',
        tasks: [
        {
            title: 'Task 1',
            description: 'Define project scope',
            status: 'Completed',
            user: { name: 'Eva Davis', role: 'Project Analyst' },
            dueDate: '2023-10-05',
            priority: 'High'
        },
        {
            title: 'Task 2',
            description: 'Conduct team training',
            status: 'Pending',
            user: { name: 'Tom Robinson', role: 'Training Specialist' },
            dueDate: '2023-10-05',
            priority: 'Medium'
        }
        ],
        createdBy: { name: 'Admin', role: 'Administrator' },
        createdAt: '2023-01-03',
        updatedAt: '2023-05-03'
    }, 
    ..... #it have more results but should be bad to visualize
    ``` 


+ Listar todas as tarefas de um usuário:
    ``` shell
    db.projects.find({ "tasks.user.name": "John Doe" });
    ```
    + Resultados:
    ``` shell	
    [
        {
            _id: ObjectId("6531d5884f303a7b6a920493"),
            name: 'Project A',
            startDate: '2023-11-11',
            endDate: '2023-12-12',
            tasks: [
                {
                    title: 'Task 1',
                    description: 'Complete initial project planning',
                    status: 'In Progress',
                    user: { name: 'John Doe', role: 'Project Manager' },
                    dueDate: '2023-10-11',
                    priority: 'High'
                },
                {
                    title: 'Task 2',
                    description: 'Develop prototype',
                    status: 'Pending',
                    user: { name: 'Jane Smith', role: 'Developer' },
                    dueDate: '2023-10-12',
                    priority: 'Medium'
                }
            ],
            createdBy: { name: 'Admin', role: 'Administrator' },
            createdAt: '2023-01-10',
            updatedAt: '2023-05-10'
        }
    ]
    ```


+ Listar todas as tarefas com status "To-Do" (a fazer) em um projeto:
    ``` shell
    db.projects.find({ "name": "Project A", "tasks.status": "Pending" });
    ```
    + Resultados:
    ``` shell
    [
        {
            _id: ObjectId("6531d5884f303a7b6a920493"),
            name: 'Project A',
            startDate: '2023-11-11',
            endDate: '2023-12-12',
            tasks: [
                {
                    title: 'Task 1',
                    description: 'Complete initial project planning',
                    status: 'In Progress',
                    user: { name: 'John Doe', role: 'Project Manager' },
                    dueDate: '2023-10-11',
                    priority: 'High'
                },
                {
                    title: 'Task 2',
                    description: 'Develop prototype',
                    status: 'Pending',
                    user: { name: 'Jane Smith', role: 'Developer' },
                    dueDate: '2023-10-12',
                    priority: 'Medium'
                }
            ],
            createdBy: { name: 'Admin', role: 'Administrator' },
            createdAt: '2023-01-10',
            updatedAt: '2023-05-10'
        }
    ]	
    ``` 


+ Listar todas as tarefas com status "To-Do" (a fazer) de um usuário:
    ``` shell
    db.projects.find({ "tasks.user.name": "John Doe", "tasks.status": "Pending" });
    ```

    + Resultados:
    ``` shell
    [
        {
            _id: ObjectId("6531d5884f303a7b6a920493"),
            name: 'Project A',
            startDate: '2023-11-11',
            endDate: '2023-12-12',
            tasks: [
                {
                    title: 'Task 1',
                    description: 'Complete initial project planning',
                    status: 'In Progress',
                    user: { name: 'John Doe', role: 'Project Manager' },
                    dueDate: '2023-10-11',
                    priority: 'High'
                },
                {
                    title: 'Task 2',
                    description: 'Develop prototype',
                    status: 'Pending',
                    user: { name: 'Jane Smith', role: 'Developer' },
                    dueDate: '2023-10-12',
                    priority: 'Medium'
                }
                ],
                createdBy: { name: 'Admin', role: 'Administrator' },
                createdAt: '2023-01-10',
                updatedAt: '2023-05-10'
        }
    ]
    ```


+ Listar todas as tarefas com prazo de entrega vencido:
    ``` shell
    db.projects.find({ "tasks.dueDate": { $lt: new Date() }, "tasks.status": { $ne: "Completed" } });
    ```

    + Resultados:
    ``` shell
    N/A
    ```


+ Encontrar todos os projetos criados pela role de um usuário:
    ``` shell
    db.projects.find({ "createdBy.role": "User" });
    ```

    + Resultados:
    ``` shell
    N/A
    ```


+ Listar todas as tarefas de um projeto ordenadas por prioridade:
    ``` shell
    db.projects.find({ "name": "Project A" }, { "tasks": { $elemMatch: { $exists: true } } }).sort({ "tasks.priority": -1 });
    ```

    + Resultados:
    ``` shell
    [
        {
            _id: ObjectId("6531d5884f303a7b6a920493"),
            tasks: [
                {
                    title: 'Task 1',
                    description: 'Complete initial project planning',
                    status: 'In Progress',
                    user: { name: 'John Doe', role: 'Project Manager' },
                    dueDate: '2023-10-11',
                    priority: 'High'
                }
            ]
        }
    ]
    ```


+ Encontrar todas as tarefas de um usuário em andamento:
    ```shell
    db.projects.find({ "tasks.user.name": "John Doe", "tasks.status": "In Progress" });
    ```

    + Resultados:
    ``` shell
    [
        {
            _id: ObjectId("6531d5884f303a7b6a920493"),
            name: 'Project A',
            startDate: '2023-11-11',
            endDate: '2023-12-12',
            tasks: [
                {
                    title: 'Task 1',
                    description: 'Complete initial project planning',
                    status: 'In Progress',
                    user: { name: 'John Doe', role: 'Project Manager' },
                    dueDate: '2023-10-11',
                    priority: 'High'
                },
                {
                    title: 'Task 2',
                    description: 'Develop prototype',
                    status: 'Pending',
                    user: { name: 'Jane Smith', role: 'Developer' },
                    dueDate: '2023-10-12',
                    priority: 'Medium'
                }
            ],
            createdBy: { name: 'Admin', role: 'Administrator' },
            createdAt: '2023-01-10',
            updatedAt: '2023-05-10'
        }
    ]
    ```


+ Listar todos os projetos criados em uma data específica:
    ```shell
    db.projects.find({ "createdAt": "2023-01-05" });
    ```

    + Resultados:
    ``` shell
    [
        {
            _id: ObjectId("6531d5884f303a7b6a920489"),
            name: 'Project DD',
            startDate: '2023-06-11',
            endDate: '2023-07-10',
            tasks: [
                {
                    title: 'Task 1',
                    description: 'Conduct market research',
                    status: 'Completed',
                    user: { name: 'Isaac Smith', role: 'Market Analyst' },
                    dueDate: '2023-07-10',
                    priority: 'High'
                },
                {
                    title: 'Task 2',
                    description: 'Develop product prototypes',
                    status: 'In Progress',
                    user: { name: 'Emma Davis', role: 'Product Designer' },
                    dueDate: '2023-07-12',
                    priority: 'Medium'
                }
            ],
            createdBy: { name: 'Admin', role: 'Administrator' },
            createdAt: '2023-01-05',
            updatedAt: '2023-01-12'
        }
    ]
    ```

+ Listar todas as tarefas de um projeto criadas entre duas datas:
    ```shell
    db.projects.find({
    "name": "Project A",
    "tasks.createdAt": { $gte: "01/10/2023", $lte: "31/12/2023" }
    });
    ```

    + Resultados:
    ``` shell
    N/A
    ```


+ Encontrar todos os usuários associados a um projeto:
    ```shell
    db.projects.aggregate([
    { $match: { "name": "Project A" } },
    { $unwind: "$tasks" },
    { $replaceRoot: { newRoot: "$tasks.user" } },
    { $group: { _id: "$name", users: { $addToSet: "$$ROOT" } } }
    ]);
    ```

    + Resultados:
    ``` shell
    [
        {
            _id: 'John Doe',
            users: [ { name: 'John Doe', role: 'Project Manager' } ]
        },
        {
            _id: 'Jane Smith',
            users: [ { name: 'Jane Smith', role: 'Developer' } ]
        }
    ]
    ```


+ Listar todas as tarefas de um projeto com descrição contendo uma palavra-chave:
    ```shell
    db.projects.find({
    "name": "Project A",
    "tasks.description": { $regex: /initial project planning/i }
    });
    ```

    + Resultados:
    ``` shell
    [
        {
            _id: ObjectId("6531d5884f303a7b6a920493"),
            name: 'Project A',
            startDate: '2023-11-11',
            endDate: '2023-12-12',
            tasks: [
                {
                    title: 'Task 1',
                    description: 'Complete initial project planning',
                    status: 'In Progress',
                    user: { name: 'John Doe', role: 'Project Manager' },
                    dueDate: '2023-10-11',
                    priority: 'High'
                },
                {
                    title: 'Task 2',
                    description: 'Develop prototype',
                    status: 'Pending',
                    user: { name: 'Jane Smith', role: 'Developer' },
                    dueDate: '2023-10-12',
                    priority: 'Medium'
                }
            ],
            createdBy: { name: 'Admin', role: 'Administrator' },
            createdAt: '2023-01-10',
            updatedAt: '2023-05-10'
        }
    ]
    ```
