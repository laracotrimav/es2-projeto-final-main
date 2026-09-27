# Melhorias de Legibilidade

Foram realizadas três melhorias de categorias diferentes.

## 1. Naming

**Commit:** `c7bac0a`

**Mensagem:** `refactor(forum): fix involved users naming`

**Antes:**

```python
invovled_users
```

**Depois:**

```python
involved_users
```

O nome foi corrigido para eliminar um erro de digitação e tornar a variável mais clara.

## 2. Style

**Commit:** `5ca3897`

**Mensagem:** `refactor(forum): simplify tracker control flow`

**Antes:**

```python
if read_cutoff is None or self.last_post is None:
    logger.debug("Readtracker is disabled.")
    return False

elif read_cutoff > self.last_post.date_created:
    logger.debug("Topic is below the read_cutoff (too old).")
    return False
```

**Depois:**

```python
if read_cutoff is None or self.last_post is None:
    logger.debug("Readtracker is disabled.")
    return False

if read_cutoff > self.last_post.date_created:
    logger.debug("Topic is below the read_cutoff (too old).")
    return False
```

O `elif` foi substituído por `if` porque a primeira condição já encerra a função com `return`. Isso deixa o fluxo de controle mais direto.

## 3. Exception Handling

**Commit:** `8e80ad6`

**Mensagem:** `refactor(forum): clarify second post exception handling`

**Antes:**

```python
try:
    return self.posts[-2].id
except IndexError:
    return None
```

**Depois:**

```python
try:
    second_last_post = self.posts[-2]
except IndexError:
    return None

return second_last_post.id
```

A alteração deixa mais claro que somente o acesso ao segundo post está protegido pelo `try`, mantendo o mesmo comportamento.