# Plano de Refactoring

Foram selecionados quatro smells para refatoração.

## 1. Duplicated Code

**Smell:** código duplicado em `Category.get_all()` e `Category.get_forums()`.

**Refactoring:** Extract Method.

**Plano:** criar um método auxiliar responsável por selecionar o `forum_alias` de acordo com o usuário.

**Resultado esperado:** a lógica duplicada ficará centralizada em um único método, reduzindo repetição e mantendo o comportamento existente.

**Risco:** alterar sem querer a lógica de seleção de fóruns para usuários autenticados ou convidados.

## 2. Long Method

**Smell:** `Forum.update_read()` concentra a consulta usada para calcular o número de tópicos não lidos.

**Refactoring:** Extract Method.

**Plano:** extrair a consulta para um método auxiliar `_get_unread_count()`.

**Resultado esperado:** `update_read()` ficará menor e com responsabilidades mais claras.

**Risco:** alterar algum filtro ou condição da consulta durante a extração.

## 3. Dead Code

**Smell:** `else` inalcançável em `Topic.update_read()`.

**Refactoring:** Remove Dead Code.

**Plano:** remover o bloco `else` que nunca pode ser executado.

**Resultado esperado:** eliminar código desnecessário sem modificar o comportamento da função.

**Risco:** muito baixo, pois o fluxo anterior já cobre todas as possibilidades.

## 4. Complex Conditional

**Smell:** condição extensa em `Topic.tracker_needs_update()`.

**Refactoring:** Extract Variable.

**Plano:** armazenar a expressão booleana em uma variável com nome descritivo.

**Resultado esperado:** tornar mais clara a intenção da condição sem alterar sua lógica.

**Risco:** alterar acidentalmente a combinação dos operadores booleanos durante a extração.