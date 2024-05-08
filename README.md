# Documentação do Banco de Dados (Marcelo Conde Filho)

## Visão Geral

Este documento descreve o esquema de banco de dados para um site da Dell com a funçâo armazenar manuais técnicos. O esquema inclui tabelas para armazenar informações sobre autores, usuários, manuais, versões dos manuais e favoritos dos usuários.

## Tabelas

### 1. Autores

Armazena informações sobre os autores dos manuais.

- **AutorID** (`Integer`): Identificador único para cada autor, chave primária, autoincremento.
- **Nome** (`Varchar(255)`): Nome do autor.
- **Contato** (`Varchar(255)`): Informações de contato do autor, opcional.

### 2. Usuarios

Gerencia os dados dos usuários que acessam o site.

- **UsuarioID** (`Integer`): Identificador único para cada usuário, chave primária, autoincremento.
- **Email** (`Varchar(255)`): Email do usuário, deve ser único.
- **Senha** (`Varchar(255)`): Senha para acesso ao site.
- **Tipo** (`Enum`): Tipo de usuário, valores possíveis são 'Administrador' e 'Usuario'.

### 3. Manuais

Contém informações sobre os manuais disponíveis no site.

- **ManualID** (`Integer`): Identificador único para cada manual, chave primária, autoincremento.
- **Titulo** (`Varchar(255)`): Título do manual.
- **Descricao** (`Text`): Descrição detalhada do manual, opcional.

### 4. Versoes

Detalha as diferentes versões de cada manual.

- **VersaoID** (`Integer`): Identificador único para cada versão, chave primária, autoincremento.
- **ManualID** (`Integer`): Chave estrangeira ligada à tabela Manuais.
- **Data** (`Date`): Data de publicação da versão.
- **NumeroVersao** (`Varchar(50)`): Número ou identificação da versão.
- **AutorID** (`Integer`): Chave estrangeira ligada à tabela Autores.

### 5. Favoritos

Permite aos usuários marcar versões específicas de manuais como favoritas.

- **UsuarioID** (`Integer`): Chave estrangeira ligada à tabela Usuarios.
- **VersaoID** (`Integer`): Chave estrangeira ligada à tabela Versoes.

## Relacionamentos

- **Autores-Versões**: Relação 1:N entre Autores e Versoes, indicando que um autor pode escrever várias versões, mas cada versão possui apenas um autor.
- **Manuais-Versões**: Relação 1:N entre Manuais e Versoes, demonstrando que um manual pode ter várias versões.
- **Usuarios-Favoritos**: Relação N:N entre Usuarios e Versoes, facilitada pela tabela Favoritos, permitindo que usuários possam favoritar múltiplas versões.
