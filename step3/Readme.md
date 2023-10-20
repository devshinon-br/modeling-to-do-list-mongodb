# Criação do Banco de Dados e Coleção

### Comandos Shell

```shell
$ mongod 
$ mongosh #em outro terminal
```

### Queries para criação
```shell
$ use todo_list #cria o db caso não exista
$ db.createCollection("projects", {
   validator: {
      $jsonSchema: {
         bsonType: "object",
         required: ["name", "startDate", "endDate", "tasks", "createdBy", "createdAt", "updatedAt"],
         properties: {
            name: {
               bsonType: "string",
               description: "Deve ser uma string e é obrigatório."
            },
            startDate: {
               bsonType: "string",
               description: "Deve ser uma data e é obrigatório."
            },
            endDate: {
               bsonType: "string",
               description: "Deve ser uma data e é obrigatório."
            },
            tasks: {
               bsonType: "array",
               description: "Deve ser um array e é obrigatório.",
               items: {
                  bsonType: "object",
                  required: ["title", "description", "status", "user", "dueDate", "priority"],
                  properties: {
                     title: {
                        bsonType: "string",
                        description: "Deve ser uma string e é obrigatório."
                     },
                     description: {
                        bsonType: "string",
                        description: "Deve ser uma string e é obrigatório."
                     },
                     status: {
                        bsonType: "string",
                        description: "Deve ser uma string com valores 'In Progress', 'Pending' ou 'Completed' e é obrigatório.",
                        enum: ["In Progress", "Pending", "Completed"]
                     },
                     user: {
                        bsonType: "object",
                        required: ["name", "role"],
                        properties: {
                           name: {
                              bsonType: "string",
                              description: "Deve ser uma string e é obrigatório."
                           },
                           role: {
                              bsonType: "string",
                              description: "Deve ser uma string e é obrigatório."
                           }
                        }
                     },
                     dueDate: {
                        bsonType: "string",
                        description: "Deve ser uma data e é obrigatório."
                     },
                     priority: {
                        bsonType: "string",
                        description: "Deve ser uma string com valores 'High', 'Medium' ou 'Low' e é obrigatório.",
                        enum: ["High", "Medium", "Low"]
                     }
                  }
               }
            },
            createdBy: {
               bsonType: "object",
               required: ["name", "role"],
               properties: {
                  name: {
                     bsonType: "string",
                     description: "Deve ser uma string e é obrigatório."
                  },
                  role: {
                     bsonType: "string",
                     description: "Deve ser uma string e é obrigatório."
                  }
               }
            },
            createdAt: {
               bsonType: "string",
               description: "Deve ser uma data e é obrigatório."
            },
            updatedAt: {
               bsonType: "string",
               description: "Deve ser uma data e é obrigatório."
            }
         }
      }
   }
})
```
