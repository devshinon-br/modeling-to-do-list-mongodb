# Estrutura do projeto

Este documento descreve a estrutura do projeto, que é composta pelos seguintes elementos:

+ Nome do projeto
+ Data de início do projeto
+ Data de término do projeto
+ Lista de tarefas
+ Informações sobre o criador do projeto

### Nome do projeto

O nome do projeto é uma string que identifica o projeto. Deve ser um nome curto e descritivo.

### Data de início do projeto

A data de início do projeto é uma string no formato "yyyy-mm-dd" que indica a data em que o projeto começou.

### Data de término do projeto

A data de término do projeto é uma string no formato "yyyy-mm-dd" que indica a data em que o projeto deve ser concluído.

### Lista de tarefas

A lista de tarefas é um array de objetos que descrevem as tarefas associadas ao projeto. Cada objeto de tarefa possui os seguintes elementos:

+ Título da tarefa
+ Descrição detalhada da tarefa
+ Status atual da tarefa
+ Informações sobre o usuário responsável pela tarefa
+ Data de vencimento da tarefa
+ Prioridade da tarefa

### Título da tarefa

O título da tarefa é uma string que identifica a tarefa. Deve ser um título curto e descritivo.

### Descrição detalhada da tarefa

A descrição detalhada da tarefa é uma string que fornece informações mais detalhadas sobre a tarefa.

### Status atual da tarefa

O status atual da tarefa é uma string que indica o status atual da tarefa. Os status possíveis são:

+ Em andamento
+ Pendente
+ Concluída

### Informações sobre o usuário responsável pela tarefa

As informações sobre o usuário responsável pela tarefa são um objeto que possui os seguintes elementos:

+ Nome do usuário
+ Cargo ou função do usuário no projeto

### Data de vencimento da tarefa

A data de vencimento da tarefa é uma string no formato "yyyy-mm-dd" que indica a data em que a tarefa deve ser concluída.

### Prioridade da tarefa

A prioridade da tarefa é uma string que indica a prioridade da tarefa. As prioridades possíveis são:

+ Alta
+ Média
+ Baixa

### Informações sobre o criador do projeto

As informações sobre o criador do projeto são um objeto que possui os seguintes elementos:

+ Nome do criador do projeto
+ Cargo ou função do criador do projeto

### Data de criação do projeto

A data de criação do projeto é uma string no formato "yyyy-mm-dd" que indica a data em que o projeto foi criado.

### Data da última atualização do projeto

A data da última atualização do projeto é uma string no formato "yyyy-mm-dd" que indica a data em que o projeto foi atualizado pela última vez.

## Exemplo de projeto

Aqui está um exemplo de projeto:

```json {
  "name": "Projeto A",
  "startDate": "2023-01-02",
  "endDate": "2023-01-29",
  "tasks": [
    {
      "title": "Tarefa 1",
      "description": "Concluir o planejamento inicial do projeto",
      "status": "Em andamento",
      "user": {
        "name": "John Doe",
        "role": "Project Manager"
      },
      "dueDate": "2023-01-25",
      "priority": "Alta"
    }
  ],
  "createdBy": {
    "name": "Admin",
    "role": "Administrator"
  },
  "createdAt": "2022-10-10",
  "updatedAt": "2023-01-26"
}
