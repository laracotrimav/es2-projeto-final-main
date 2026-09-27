# Retrospectiva

## Evolução do projeto

Na Parte 1, o foco principal foi entender o código existente e aumentar a segurança para fazer alterações. O módulo `flaskbb/user/` tinha cobertura de linhas de 30,7%, e foram adicionados testes unitários e casos parametrizados sem alterar o comportamento da aplicação. Ao final dessa etapa, a cobertura chegou a 33,0% e a suíte continuou passando normalmente.

Na Parte 2, o trabalho foi direcionado para identificação de code smells, refatoração e legibilidade. Foram analisados problemas como métodos longos, código duplicado, código morto e condições complexas. Também foram feitas melhorias de nomenclatura, fluxo de controle e tratamento de exceções. O objetivo principal foi entender que uma alteração em um sistema legado precisa ser pequena, testada e feita sem comprometer o comportamento existente.

Na Parte 3, a análise do `flaskbb/user/` mostrou suas dependências com modelos do fórum, banco de dados, serviços, plugins e outras partes da aplicação. Também foi possível identificar pontos de acoplamento, fragilidades e lugares onde seria possível introduzir seams para facilitar futuras alterações e testes. A proposta de evolução foi a criação gradual de uma camada de repositórios, separando melhor a lógica de negócio do acesso à persistência.

## Técnicas mais úteis

A técnica mais útil foi o uso de testes como apoio às mudanças. Antes de fazer qualquer alteração, executar a suíte e depois executá-la novamente ajudou a verificar se o comportamento continuava preservado. Isso foi especialmente importante nas refatorações da Parte 2, porque algumas mudanças pareciam simples, mas poderiam afetar outras partes do sistema.

A identificação de code smells também foi bastante útil para enxergar problemas que não são necessariamente erros, mas dificultam a manutenção. Um exemplo foi a duplicação de código encontrada em métodos relacionados às categorias do fórum. Outro exemplo foi a remoção de um trecho de código morto que não poderia ser executado.

Entretanto, a parte mais complexa foi analisar o sistema sem conhecer previamente toda a sua arquitetura. Em um projeto menor, as dependências são mais fáceis de acompanhar. No FlaskBB, uma operação aparentemente simples pode envolver models, services, plugins, banco de dados e outras partes da aplicação. Por isso, a leitura do código e a identificação das relações entre os módulos exigiram mais atenção do que simplesmente alterar uma função.

## O que faria de diferente

Se eu começasse o projeto novamente, faria um mapeamento mais completo dos módulos logo no início. Isso ajudaria a entender melhor as dependências antes de escolher onde trabalhar e evitaria ter que descobrir algumas relações somente durante as etapas posteriores.

Também dedicaria mais tempo inicialmente à leitura dos testes existentes. Eles ajudam a mostrar não apenas o que o código faz, mas também quais comportamentos são considerados importantes pela aplicação.

Por fim, manteria a mesma ideia de fazer mudanças pequenas e sempre validá-las com os testes. Trabalhar dessa forma mostrou que, em um sistema legado, melhorar o código não significa necessariamente reescrevê-lo. Muitas vezes, pequenas mudanças bem justificadas já tornam o sistema mais fácil de entender, testar e evoluir.