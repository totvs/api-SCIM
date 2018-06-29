# API SCIM TOTVS

## Introdução

O SCIM 'users' é um protocolo de aplicação REST para provisionamento e gerenciamento de dados de identidade na web. O protocolo suporta a criação, modificação, recuperação e descoberta de usuários.

O serviço users do Protheus permite a inclusão e manipulação de dados de usuário no sistema. É altamente aconselhável que a autenticação de serviços esteja habilitada no servidor rest para evitar manipulação indevida dos dados. Todos os usuários que se autenticarem para utilizar este serviço devem possuir acesso a rotina CFGA510 (o cadastro de usuários no Protheus)

Detalhes da configuração do REST Protheus e como ligar a autenticação dos serviços acesse a página do REST Protheus <a href="http://tdn.totvs.com/pages/viewpage.action?pageId=75268866)" target="_blank">aqui</a>.

> **Atenção**  
> Via REST apenas é possível a criação básica do usuário. Para configurar permissões, acessos, menus, etc, é necessária a utilização do Identity.

## Métodos

### GET pelo ID [/users/{userId}/{?showAdmin,count,startIndex,attributes}]

Para recuperar um usuário conhecido, os clientes enviam requisições GET. Se o usuário existir o servidor responde com o código de estado 200 e inclui o resultado no corpo da resposta. Também é possível listar os usuários do sistema, omitindo o envio do _pathParam {userId}_.

> A busca por um usuário passando o Id difere apenas da omissão no resultado dos parâmetros totalResult, itensPerPage e startIndex.

+ Parameters
  + userId (string) - id ou código do usuário no sistema.
  + showAdmin (boolean, optional) - Indica se o get deve retornar o usuário admin. - Default: false
  + count (numérico, optional) - Indica quantos usuários deverão ser retornados pelo método. - Default: Todos
  + startIndex (numérico, optional) - Indica a partir de qual usuário encontrado deverá ocorrer o retorno. - Default: 1
  + attributes (string, optional) - Indica quais atributos do jSon devem ser retornados. Os atributos devem ser separados por ','. - Default: Retorna todos os atributos
    + O parâmetro **attributes** é case sensitive.

### POST [/users/{userid}/{operation}]

Cria novos usuários no sistema devolvendo na requisição, quando bem sucedida, o código de resposta 201 (created).

+ Parameters
  + userid (string, optional) - id ou código do usuário no sistema.
  + operation (string, optional) - Valores aceitos: activate e deactivate. Indica se o usuário será ativado no sistema (activate) ou se o usuário será bloqueado via SAML (deactivate) ou se um novo usuário será criado (parâmetro vazio ou qualquer outro valor diferente dos anteriores. Caso o parâmetro userId seja enviado mas não seja enviado o parâmetro operation é assumido que um novo usuário será criado no sistema.

### PUT [/users/{userid}]

Método utilizado para atualizar um usuário existente. Todos os parâmetros podem ser enviados, tal qual o método POST.

+ Parameters
  + userid (string, required) - id ou código do usuário no sistema.

### Delete [/users/{userid}]
  
Método utilizado para bloquear um usuário existente. O usuário é bloqueado, e todos os itens amarrados ao seu registro (grupos, vínculo funcional, etc) são desassociados.

+ Parameters
  + userid (string, required) - id ou código do usuário no sistema.