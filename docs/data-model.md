#Modelo de dados

A Api tem duas entidades: pedidos (orders) e seus Itens (Itens), ligadas por um relacionamento 1:N

##Tabela: orders

| Coluna     | Tipo (SQLAlchemy)       | Tipo (PostgreSQL)        | Restricoes     |
| ---------- | ----------------------- | ------------------------ | -------------- |
| id         | String                  | VARCHAR / TEXT           | PK             |
| customer   | String                  | VARCHAR / TEXT           | NOT NULL       |
| status     | String                  | VARCHAR / TEXT           | DEFAULT 'open' |
| created_at | DateTime(timezone=True) | TIMESTAMP WITH TIME ZONE | DEFAULT now()  |

##Tabela: Itens

| Coluna      | Tipo (SQLAlchemy) | Tipo (PostgreSQL) | Restricoes   |
| ----------- | ----------------- | ----------------- | ------------ |
| id          | String            | VARCHAR / TEXT    | PK           |
| order_id    | String            | VARCHAR / TEXT    | FK, NOT NULL |
| sku         | String            | VARCHAR / TEXT    | NOT NULL     |
| description | String            | VARCHAR / TEXT    | NOT NULL     |
| quantity    | Integer           | INTEGER           | NOT NULL     |

# Relacionamento

Um pedido tem vários Itens (1:N).  
A chave estrangeira **order_id** fica na tabela **items**, referenciando **orders.id**.

O relcacionamento está declaraco com CASCADE o que significa que se um pedido for deletado, todos os seus itens também serão deletados automaticamente, e se um item for removido do pedido ele também será removido do banco.
