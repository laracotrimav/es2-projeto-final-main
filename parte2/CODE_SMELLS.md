# Code Smells

## Arquivo analisado

`flaskbb/forum/models.py`

Os smells foram identificados na versão do arquivo antes das refatorações realizadas nesta etapa.

## 1. Long Method

**Localização:** `flaskbb/forum/models.py:1407-1469` — `Category.get_all()`

```python
if user.is_authenticated:
    user_groups = [gr.id for gr in user.groups]
    user_forums = (
        db.select(Forum)
        .filter(Forum.groups.any(Group.id.in_(user_groups)))
        .subquery()
    )
    forum_alias = aliased(Forum, user_forums)
    ...
else:
    guest_group = Group.get_guest_group()
    guest_forums = (
        db.select(Forum)
        .filter(Forum.groups.any(Group.id == guest_group.id))
        .subquery()
    )
    forum_alias = aliased(Forum, guest_forums)
    ...
```

O método concentra várias responsabilidades, como seleção dos fóruns, filtragem por grupo, montagem das consultas e organização do resultado.

## 2. Duplicated Code

**Localização:** `flaskbb/forum/models.py:1421-1458` e `1484-1521` — `Category.get_all()` e `Category.get_forums()`

```python
if user.is_authenticated:
    user_groups = [gr.id for gr in user.groups]
    user_forums = (
        db.select(Forum)
        .filter(Forum.groups.any(Group.id.in_(user_groups)))
        .subquery()
    )
    forum_alias = aliased(Forum, user_forums)
```

A mesma lógica de definição de `forum_alias` aparece nos dois métodos, com pouca diferença entre os contextos.

## 3. Flag Argument

**Localização:** `flaskbb/forum/models.py:1055-1082` — `Forum.update_last_post()`

```python
def update_last_post(self, commit=True):
    ...
    if commit:
        db.session.commit()
```

O parâmetro `commit` altera o comportamento interno do método, fazendo com que a mesma função tenha dois fluxos diferentes.

## 4. Feature Envy

**Localização:** `flaskbb/forum/models.py:360-400` — `Post._deal_with_last_post()`

```python
self.topic.forum.last_post = second_last_post
self.topic.forum.last_post_title = second_last_post.topic.title
self.topic.forum.last_post_user = second_last_post.user
self.topic.forum.last_post_username = second_last_post.username
self.topic.forum.last_post_created = second_last_post.date_created
```

O método pertence a `Post`, mas manipula repetidamente diversos atributos de `self.topic.forum`, indicando que parte da responsabilidade está mais relacionada ao objeto `Forum`.

## 5. Dead Code

**Localização:** `flaskbb/forum/models.py:705-723` — `Topic.update_read()`

```python
if topicsread:
    ...
elif not topicsread:
    ...
else:
    updated = False
```

Os dois primeiros testes já cobrem as possibilidades de `topicsread` ser verdadeiro ou falso. Por isso, o `else` final nunca pode ser executado.

## 6. Complex Conditional

**Localização:** `flaskbb/forum/models.py:665-669` — `Topic.tracker_needs_update()`

```python
if (
    forumsread
    and forumsread.cleared is not None
    and forumsread.cleared >= self.last_post.date_created
):
```

A condição reúne várias verificações em uma única expressão, dificultando a leitura imediata do motivo pelo qual o método retorna `False`.