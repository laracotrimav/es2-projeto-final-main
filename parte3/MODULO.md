# Módulo `flaskbb/user/`

## Propósito

O módulo `flaskbb/user/` concentra as funcionalidades relacionadas aos usuários do fórum, reunindo os modelos de usuário e grupos, os formulários de alteração de dados, as rotas de perfil e configurações, os serviços responsáveis pelas atualizações e as integrações com o sistema de plugins. O módulo recebe ações do usuário pelas rotas, valida e processa as alterações e persiste os dados no banco.

## Arquivos principais

| Arquivo                               | Responsabilidade                                                                                               |
| ------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `flaskbb/user/__init__.py`            | Inicializa o módulo e força o carregamento dos plugins de usuário.                                             |
| `flaskbb/user/models.py`              | Define os modelos `User`, `Group` e `Guest`, além das regras relacionadas a grupos, permissões e persistência. |
| `flaskbb/user/forms.py`               | Define os formulários usados nas configurações e alterações da conta.                                          |
| `flaskbb/user/views.py`               | Define as views e rotas de perfil, configurações, senha, e-mail e dados do usuário.                            |
| `flaskbb/user/plugins.py`             | Implementa hooks relacionados ao perfil e fornece validadores para as atualizações.                            |
| `flaskbb/user/services/factories.py`  | Cria formulários e handlers usados nas operações de atualização do usuário.                                    |
| `flaskbb/user/services/update.py`     | Aplica alterações, persiste os dados e dispara eventos após as atualizações.                                   |
| `flaskbb/user/services/validators.py` | Implementa validações específicas para alterações de e-mail, senha e avatar.                                   |

## Pontos de entrada e saídas

### Entradas externas

As principais entradas do módulo são as rotas registradas em `flaskbb/user/views.py`:

* `/settings/email`
* `/settings/general`
* `/settings/password`
* `/settings/user-details`
* `/<username>/posts`
* `/<username>/topics`
* `/<username>`

As quatro primeiras exigem usuário autenticado. As outras são usadas para visualizar informações públicas do usuário. Além disso, o módulo participa do sistema de plugins por meio de hooks. `flaskbb/user/plugins.py` registra implementações para carregar links do perfil e fornecer validadores para alterações de senha, e-mail e dados do usuário.

### Saídas

As principais saídas são:

* dados de `User` e `Group` persistidos no banco de dados;
* páginas renderizadas para perfil e configurações;
* redirecionamentos após alterações;
* erros de validação apresentados nos formulários;
* eventos de plugin disparados após alterações de dados do usuário.

O módulo não possui comandos CLI próprios. Seu principal fluxo de entrada acontece pelas rotas HTTP e pela integração com o sistema de plugins.

## Docstrings adicionadas

### `User.get_permissions()`

**Arquivo:** `flaskbb/user/models.py`
**Linhas:** 361–365

A docstring explica que o método reúne as permissões dos grupos do usuário e que o parâmetro `exclude` permite retirar algumas permissões do resultado.

### `settings_form_factory()`

**Arquivo:** `flaskbb/user/services/factories.py`
**Linhas:** 62–67

A docstring explica que a função cria o formulário de configurações, configura as opções de tema e idioma e mantém os valores atuais do usuário quando o formulário ainda não foi validado com sucesso.

### `flaskbb_tpl_profile_links()`

**Arquivo:** `flaskbb/user/plugins.py`
**Linhas:** 46–47

A docstring explica que o hook adiciona os links padrão do perfil aos links fornecidos por outros plugins.