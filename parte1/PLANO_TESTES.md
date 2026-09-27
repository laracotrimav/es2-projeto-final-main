# Plano de Testes

## Módulo escolhido

O módulo escolhido foi `flaskbb/user/`. A escolha foi feita porque ele apresenta comportamentos mais isolados e permite criar testes unitários focados em funções específicas, sem necessidade de alterar o código de produção.

A cobertura inicial do módulo era de **30,7% das linhas** e **58,3% dos branches**. A meta definida foi aumentar a cobertura de linhas em pelo menos 2 pontos percentuais, chegando a pelo menos **32,7%**.

## Cenários inicialmente selecionados

| Cenário                                                                  | Tipo       |
| ------------------------------------------------------------------------ | ---------- |
| `settings_form_factory()` carrega as configurações do usuário atual      | Happy path |
| `change_password_form_factory()` cria o formulário de alteração de senha | Happy path |
| `change_email_form_factory()` associa o formulário ao usuário atual      | Happy path |
| `change_details_form_factory()` carrega os dados do usuário atual        | Happy path |
| `password_update_handler()` solicita os validadores de senha pelo hook   | Interação  |
| `details_update_factory()` cria o handler de atualização de detalhes     | Happy path |
| `email_update_handler()` cria o handler de atualização de e-mail         | Happy path |

Os cenários foram escolhidos a partir dos caminhos ainda não exercitados no módulo, principalmente nas funções de `flaskbb/user/services/factories.py`.