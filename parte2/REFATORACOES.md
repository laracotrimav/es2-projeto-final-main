# Refatorações realizadas

Foram realizadas quatro refatorações principais, cada uma registrada em um commit separado.

## 1. Extract Method — seleção do `forum_alias`

**Commit:** `67bd5ed`

**Mensagem:** `refactor(forum): extract forum alias selection`

**Smell tratado:** Duplicated Code.

**Antes:** `Category.get_all()` e `Category.get_forums()` possuíam lógica duplicada para selecionar o `forum_alias`.

**Depois:** foi criado o método auxiliar `_get_forum_alias()`, utilizado pelos dois métodos.

**Resultado:** a lógica de seleção ficou centralizada em um único ponto.

## 2. Extract Method — consulta de tópicos não lidos

**Commit:** `584ec2f`

**Mensagem:** `refactor(forum): extract unread count query`

**Smell tratado:** Long Method.

**Antes:** `Forum.update_read()` continha diretamente toda a consulta usada para calcular `unread_count`.

**Depois:** a consulta foi extraída para `_get_unread_count()` e `update_read()` passou a utilizar o método auxiliar.

**Resultado:** o método principal ficou menor e com uma responsabilidade mais clara.

> Observação: durante a aplicação dessa refatoração também foram incorporadas alterações de formatação/comentários no arquivo, sem mudança funcional no comportamento testado.

## 3. Remove Dead Code

**Commit:** `7834ee1`

**Mensagem:** `refactor(forum): remove dead code from topic read update`

**Smell tratado:** Dead Code.

**Antes:** `Topic.update_read()` possuía um `else` que não poderia ser executado.

**Depois:** o bloco inalcançável foi removido.

**Resultado:** o fluxo ficou mais simples sem alterar o comportamento.

## 4. Extract Variable — condição do tracker

**Commit:** `c597487`

**Mensagem:** `refactor(forum): extract tracker condition`

**Smell tratado:** Complex Conditional.

**Antes:** a verificação relacionada ao `ForumsRead` estava escrita diretamente dentro de um `if` com várias condições.

**Depois:** a expressão foi armazenada em uma variável chamada `forum_was_cleared_after_last_post`.

**Resultado:** a intenção da condição ficou mais clara e a lógica foi mantida.