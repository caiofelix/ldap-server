# LDAP-SERVER
Servidor LDAP (Lightweight Directory Access Protocol) para testes de desenvolvimento de aplicações que dependem de autenticação LDAP sem a necessidade de um servidor real.
Este projeto fornece um ambiente de desenvolvimento local com um servidor OpenLDAP e uma interface de administração (phpLDAPadmin) configurados com Docker.

## Funcionalidades

- **Servidor OpenLDAP**: Pronto para uso.
- **phpLDAPadmin**: Interface web para visualizar e gerenciar os dados do LDAP.
- **Estrutura de Exemplo**: Inclui arquivos (`.ldif`) com esquemas e dados de exemplo.

## Como Usar

### Pré-requisitos

- [Docker](https://www.docker.com/get-started)

### 1. Iniciar o Ambiente

Para iniciar o servidor LDAP e o phpLDAPadmin, execute o comando na raiz do projeto:

```bash
docker-compose up -d
```

### 2. Acessar os Serviços

- **Servidor LDAP**:
  - **Endereço**: `ldap://localhost:389`
  - **Base DN**: `dc=example,dc=org`
  - **DN de Administrador**: `cn=admin,dc=example,dc=org`
  - **Senha de Administrador**: `admin123`

- **phpLDAPadmin**:
  - **URL**: [http://localhost:8080](http://localhost:8080)
  - **Login DN**: `cn=admin,dc=example,dc org`
  - **Senha**: `admin123`

## Estrutura e Usuários de Exemplo

O servidor é inicializado com a seguinte estrutura:

- **Base DN**: `dc=example,dc=org`
  - **Unidade Organizacional**: `ou=people`
    - **Usuários**:
      - `cn=Test,ou=people,dc=example,dc=org`
        - **uid**: `test.user`
        - **cpf**: `01234567890`
        - **senha**: `senha123`

## Personalização

### Alterar Configurações

Você pode modificar variáveis de ambiente no arquivo `docker-compose.yml` para alterar:
- Domínio (`LDAP_DOMAIN`)
- Organização (`LDAP_ORGANISATION`)
- Senha do administrador (`LDAP_ADMIN_PASSWORD`)

### Adicionar Seus Próprios Dados

Para adicionar seus próprios esquemas ou dados (`.ldif`):

1. Crie um arquivo `.ldif` na pasta `ldif/`.
2. Os arquivos são carregados em ordem alfabética. Use prefixos numéricos para controlar a ordem.
3. Reinicie o contêiner do zero para aplicar as mudanças:

   ```bash
   docker-compose down -v && docker-compose up -d
   ```

   **Atenção**: O comando acima destrói os volumes, apagando todos os dados existentes.

## Parar o Ambiente

Para parar os contêineres sem apagar os dados:

```bash
docker-compose down
```

Para parar e apagar os dados (incluindo os volumes):

```bash
docker-compose down -v
```
