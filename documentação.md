## Diagrama de Banco de Dados

### Tabelas e Campos

#### 1. `users`
- **Ids** (integer): Chave primária única para cada usuário.
- **Names** (varchar): Nome do usuário.
- **Genders** (varchar): Gênero do usuário.
- **Emails** (varchar): E-mail do usuário.
- **Passwords** (varchar): Senha do usuário.
- **AccessLevels** (boolean): Nível de acesso do usuário (administrador ou regular).

#### 2. `AssembleLine`
- **Ids** (integer): Chave primária única para cada linha de montagem.
- **Names** (varchar): Nome da linha de montagem.
- **Descriptions** (varchar): Descrição da linha de montagem.
- **AssociatedAdministratorId** (integer): Chave estrangeira que referencia `Ids` em `users`, associando um administrador a cada linha de montagem.

#### 3. `Products`
- **Ids** (integer): Chave primária única para cada produto.
- **Names** (varchar): Nome do produto.
- **AssociatedAssembleLineId** (integer): Chave estrangeira que referencia `Ids` em `AssembleLine`, associando cada produto a uma linha de montagem específica.

#### 4. `Handbooks`
- **Ids** (integer): Chave primária única para cada manual.
- **AssociatedProductIds** (integer): Campo para armazenar IDs de produtos associados, indicando um relacionamento N:N com `Products`.
- **Names** (varchar): Nome do manual.
- **Descriptions** (varchar): Descrição do manual.
- **UploadDates** (timestamp): Data de upload do manual.
- **AdditionalFilesId** (integer): Chave estrangeira que referencia `Ids` em `AdditionalFiles`, vinculando arquivos adicionais ao manual.

#### 5. `HandbookVersion`
- **Ids** (integer): Chave primária única para cada versão do manual.
- **AssociatedPublicationDates** (timestamp): Data de publicação da versão do manual.
- **AssociatedHandbookIds** (integer): Chave estrangeira que referencia `Ids` em `Handbooks`, vinculando cada versão a um manual específico.

### Relacionamentos

- **`AssembleLine` to `users`**: Cada linha de montagem é gerenciada por um usuário administrador, criando um relacionamento 1:N entre usuários (como administradores) e linhas de montagem.
- **`Products` to `AssembleLine`**: Cada produto é produzido em uma linha de montagem específica, formando um relacionamento 1:N entre linha de montagem e produtos.
- **`Handbooks` to `Products`**: Um manual pode se aplicar a vários produtos e vice-versa, indicando um relacionamento muitos para muitos que é tratado neste caso com um campo de IDs de produtos associados em `Handbooks`.
- **`HandbookVersion` to `Handbooks`**: Cada versão está ligada a um manual específico, indicando um relacionamento 1:N entre manuais e suas versões.