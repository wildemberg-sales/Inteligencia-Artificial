## Portifólio 2

# Inteligência Artificial - Resolvendo problemas por busca 

\vspace{10cm}

---

**Autor:** Wildemberg Sales da Silva Junior

**Matrícula:** 202017503

**Data:** 24/12/2024

**Instituição/Universidade:** Universidade de Brasília(UnB)

**Disciplina:** Inteligência Artificial - FGA0221

---

\newpage

## Resumo
resumo do artigo

## Visão Geral
Visão geral do artigo

\newpage

## Introdução
Neste artigo, iremos abordar e discorrer sobre um tópico importante da área de IA(Inteligência Artificial) que serão os agentes de resolução de problemas por meio de busca, em que vemos como um agente pode encontrar uma sequência de ações que alcança seus objetivos quando nenhuma ação isolada é capaz de fazê-lo (RUSSEL; NORVIG, 2010).    
No decorrer do artigo entenderemos o que são esses agentes de resolução de problemas, os ambientes em que eles atuam, os problemas que são capazes de resolver, tipos de algoritmos de busca para resolução de problemas em ambientes simples ou complexos, entre outros temas.   
A seguir, iremos começar os nossos estudos entendendo o que são agentes de soluções de problemas, que será o tema base para o nosso artigo.

## Agente de resolução de problemas
Agentes de resolução de problemas são agentes baseados em objetivos que se diferenciam de agentes mais simples pelo fator de considerarem ações futuras e o quanto seus resultados são desejáveis. Outra característica importante dos agentes de resolução de problemas é que eles se utilizam de representações atômicas, onde os estados do mundo são considerados como um todo sem estrutura interna visível para os algoritmos (RUSSEL; NORVIG, 2010).

É importante entender que agentes inteligentes maximizam suas medidas de desempenho ao tomar decisões baseadas na meta de atingir seu objetivo, com isso esses agentes simplificam seus problemas de decisão ao definir um objetivo específico, tornando a resolução de problemas mais fácil de se gerenciar.  

Um ponto que devemos entender é a definição de objetivos e a formulação de problemas realizadas pelos agentes, pois são a chave para a resolução de problemas. Os objetivos são definidos como um conjunto de estados desejados no mundo, onde esses estados são os necessários para que o objetivo seja satisfeito, com isso o agente deve se verificar esses estados e entender como ele irá chegar no estado do objetivo, analisando as ações necessárias e os estados intermediários que levam ao estado objetivo. Com esses dados em análise o agente pode então realizar a formulação do problema que vai fornecer uma visão geral para o agente sobre quais ações, decisões e estados são os corretos e mais eficientes para alcançar o objetivo.

Um agente pode ou não ter informações disponíveis para tomar suas decisões, com isso, se pensarmos em um agente que tem o objetivo de ir de um **ponto A** a um **ponto B**, e possui diversas rotas disponíveis para cumprir seu objetivo, se não possuir informações sobre as rotas, o método que será adotado pelo agente é tentar caminhos aleatórios até cumprir o seu objetivo, mas, se o agente possuir informações sobre as rotas como distância, semáforos, desvios e etc, ele pode otimizar seu modo de agir, prevendo ações futuras e planejando uma sequência de ações otimizadas para chegar ao objetivo.

Para que seja possível o agente poder analisar ações futuras, o ambiente em que o agente está inserido deve possuir as seguintes propriedades:

* Observável: Onde o agente sempre conhece o estado atual;
* Discreto: Onde existe um número finito de ações disponíveis em cada estado em que o agente se encontra; 
* Conhecido: O agente sabe o resultado das ações que ele tomar;
* Determinístico: Cada ação que o agente tomar leva a um único resultado;

Com essas características de ambientes bem definidas, é possível afirmar que a solução para um problema é uma sequência fixa de ações  (RUSSEL; NORVIG, 2010). Vale ressaltar que essa premissa é relacionada a ambientes previsíveis, em ambiente menos previsíveis, pode haver uma complexidade maior para chegar ao seu objetivo. Um agente que realiza seu planjamento de forma a ignorar o restante do ambiente, deve estar completamente certo do que está acontecendo, isso se chama de um sistema de **malha aberta**, pois ignorar a percepção quebra o laço entre o agente e o ambiente.

## Problemas de malha aberta e de malha fechada
Neste tópicos iremos abordar problemas de malha aberta e fechada, a fim de entender as diferenças das ações de um agente nesses modelos.

Antes de analisarmos os problemas, é interessante entendermos a diferença entre **malha aberta** e **malha fechada**. 

* **Malha Aberta**: Quando o agente executa o plano previamente definido com base nas informações do ambiente, e executa o plano cegamente ignorando as novas percepções do ambiente, ou seja, ele não se adapta a novas alterações do ambiente;
* **Malha Fechada**: Quando o agente executa o planjedo, mas continua a observar o ambiente e se adaptar a ele, fazendo os ajustes em suas ações futuras.

Com esses dois modelos definidos, podemos agora obervar um exemplo de problema com dois modelos, onde no **exemplo 1.1** iremos analisar a resolução do problema com malha aberta, e no **exemplo 1.2** a resolução do problema com malha fechada. Para basear os exemplos, o contexto será o seguinte: 
> Um agente pertencente a uma esteira de linha de montagem, deve realizar a montagem de um equipamento, para o agente é fornecido um manual de intruções sobre a montagem de cada peça, e qual peça depende de outra.

**Exemplo 1.1 - Malha Aberta**

Se o agente executar suas ações em um modelo de malha aberta, ele irá analisar o documento fornecido com as intruções de montagem, as dependências de peças, e qual a melhor ordem de montagem, com isso, ele irá traçar um plano para executar em ordem um conjunto de ações e chegar ao seu objetivo.

Se não houver problemáticas na montagem do equipamento, tudo ocorrerá muito bem, e o agente irá conseguir terminar a montagem da maneira que planejou. Mas, se alguma peça do equipamento quebrar durante o processo e não servir para utilização, o agente não conseguirá terminar sua montagem, pois ele não tem a capacidade de mudar seu planejamento devido a esse incidente.

A seguir podemos ver a aplicação do algoritmo do agente:

````text
ALGORITMO Montagem_Malha_Aberta
    ENTRADA: instrucoes, pecas_disponiveis
    PARA cada etapa EM instrucoes:
        peca <- etapa.peca
        dependencias <- etapa.dependencias

        SE dependencias NÃO ESTÃO em pecas_disponiveis:
            EXIBIR "Erro: Dependências para a peça {peca} não estão disponíveis."
            ENCERRAR

        SE peca NÃO ESTÁ em pecas_disponiveis:
            EXIBIR "Erro: A peça {peca} está quebrada. Não é possível continuar."
            ENCERRAR

        REMOVER peca DE pecas_disponiveis
        EXIBIR "Montando a peça {peca}."

    EXIBIR "Montagem concluída com sucesso."
FIM_ALGORITMO
````
<figcaption align="center"><b>Código 1</b>: Algoritmo do agente executando em malha aberta. Fonte: OPENAI. Assistente Virtual ChatGPT, 2024</figcaption>

**Exemplo 1.2 - Malha Fechada**

Se o agente executar suas ações baseado no modelo de malha fechada, ele irá analisar o documento fornecido com as instruções de montagem, mas depencências das peças, e qual a melhor ordem de montagem para chegar ao objetivo da forma mais otimizada.

Se não houver problemáticas o agente conseguirá chegar ao seu objetivo. Mas supondo que ocorra o mesmo problema do exemplo 1.1, onde durante a montagem uma das peças acabou se quebrando, o agente irá realizar uma nova análise das formas de contornar esse problema, seja solicitando uma nova peça para a esteira de produção, ou ajustando seu plano para montar o equipamento sem e peça, ou deixando a montagem da peça quebrada para o final. Todas essas formas podem ser utilizadas pelo agente para continuar as ações para alcançar o objetivo, pois ele analisou os estados em que se encontrava e ajustou suas ações para isso.

A seguir temos a aplicação do algoritmo do agente:

````text
ALGORITMO Montagem_Malha_Fechada
    ENTRADA: instrucoes, pecas_disponiveis
    PARA cada etapa EM instrucoes:
        peca <- etapa.peca
        dependencias <- etapa.dependencias

        ENQUANTO dependencias NÃO ESTÃO em pecas_disponiveis:
            EXIBIR "Aguardando dependências para a peça {peca}."
            ADICIONAR dependencias PARA pecas_disponiveis

        ENQUANTO peca NÃO ESTÁ em pecas_disponiveis:
            EXIBIR "A peça {peca} está quebrada. Solicitando nova peça."
            ADICIONAR peca PARA pecas_disponiveis

        REMOVER peca DE pecas_disponiveis
        EXIBIR "Montando a peça {peca}."

    EXIBIR "Montagem concluída com sucesso."
FIM_ALGORITMO
````
<figcaption align="center"><b>Código 2</b>: Algoritmo do agente executando em malha fechada. Fonte: OPENAI. Assistente Virtual ChatGPT, 2024</figcaption>

## Algoritmos de busca
Como foi visto anteriormente, agentes inteligentes fazem um planejamento para chegar ao seu objetivo, este planejamento é feito baseado no entendimento do ambiente e através da previsão se ações e estados futuros em que o agente pode estar, com isso, se nos aprofundarmos no planejamento das ações do agente, será possível entender que é composto por uma série de buscas que analisam várias sequências de ações possíveis.

Essas séries de buscas realizadas pelo agente que analisam diversas sequências de ações para identificar a melhor que chegará ao objetivo, acaba gerando uma árvore de busca, onde tal árvore possui na raiz o estado inicial do agente, em suas ramificações existem as possíveis ações, e nos nós os estados possíveis que o agente pode estar. Os agentes percorrem essas árvores de busca diversas vezes para analisar e compreender qual a melhor "rota" possível para chegar ao objetivo.

No decorrer desta seção iremos abordar dois importante tópicos de busca, a **busca cega** e a **busca informada**, que trazem aspectos e modelos diferentes de atuação de um agente na resolução de um problema.

### Busca Cega
A busca cega ou busca sem informação, é um modelo de busca realizado pelo agente, onde ele não tem nenhuma informação adicional sobre os estados do ambiente, além das informações que recebeu na definição do problema, ou seja, ele não tem uma "visão" privilegiada sobre os estados mais promissores a serem explorados, portanto esses agentes funcionam apenas com a capacidade de gerar sucessores e distinguir se chegaram ao objetivo ou não.

Dentro deste modelo de busca cega, temos alguns submodelos que possuem características e funcionamentos diferentes, a seguir vamos entender um pouco mais sobre eles:

* **Busca em Largura:** Este modelo de busca expande todos os nós da árvore de busca, independente se durante o processo já encontrou o estado objetivo, ele segue um padrão de abrir todos os nós de um nível, antes de expandir os nós de outro nível. Isso garante que o agente sempre encontre o melhor caminho para se chegar ao objetivo
* **Busca de Custo Uniforme:** Este modelo é parecido com o de busca em largura, mas com uma pequena diferença, ele não expande todos os nós de um nível, ele expande os nós com o menos custo de caminho, este modelo armazena através de uma fila de prioridade os custos e prioriza os de menor valor.
* **Busca em Profundidade:** Este modelo realiza um tipo de busca diferente dos citados anteriormente, ele realiza uma busca através de uma das ramificações até chegar no objetivo ou ao final da ramificação, caso ele encontre o final, ele volta um nível, e abre as ramificações. De forma mais simples, podemos pensar que ele vai sempre seguindo uma direção da árvore, por exemplo, em todo nó, ele sempre continua seguindo à esquerda, até que chegue ao final ou ao objetivo, caso chegue ao final, ele volta um nível, e começa a pegar a direita, e assim por diante até percorrer toda a árvore, ou até encontrar o objetivo. Uma diferença deste modelo para os anteriores, é que ele não garante o melhor caminho até o objetivo.
* **Busca de Bidirecional:** Este modelo aplica uma lógica de encontro de buscas, onde a sua busca é iniciada em dois lugares, uma na raiz da árvore e uma no objetivo, e essas buscas devem se encontrar em um caminho intermediário.
* **Busca de Profundidade Limitada:** Este modelo é o mesmo do de busca em profundidade, a diferença entre eles é que este modelo tem um limite de nível, onde caso ele chegue a esse limite, ele volta um nível e contiua sua busca. De forma simples, é como se fosse definido onde é o "final" da árvore.

### Algoritmo desenvolvido de busca cega
Um dos algoritmos não discutidos em sala de aula é o de busca de profundidade limitada que pode ser encontrada em RUSSELL, Stuart; NORVIG, Peter. *Inteligência Artificial: Uma Abordagem Moderna*, página 123. O algoritmo base para implementação do *código 3* pode ser encontrado no mesmo livro na figura 3.17, páginas 120 e 121. Esse algoritmo apresenta a modelagem do método de busca de profundidade limitada.

````python
def busca_em_profundidade_limitada(problema, limite):
    return bpl_recursiva(problema, limite)

def bpl_recursiva(problema, limite):
    if is_goal(problema):
        return problema
    elif limite == 0:
        return "corte"
    else:
        corte_ocorrido = False
        for filho in expand(problema):
            resultado = bpl_recursiva(filho, limite - 1)
            if resultado == "corte":
                corte_ocorrido = True
            elif resultado is not None:
                return resultado
        return "corte" if corte_ocorrido else None
````
<figcaption align="center"><b>Código 3</b>: Implementação do algoritmo de busca de profundidade limitada.</figcaption>

### Busca Informada
A busca informada se dá quando o agente tem informações a mais sobre o ambiente e os estados que ele pode possuir ou possui. De forma simplificada podemos pensar na idéia de ir de uma cidade a outra com um mapa, onde o agente teria as informações sobre os caminhos que ele pode percorrer como distância, desvios, problemas e etc.


### Algoritmo desenvolvido de busca informada
### Algoritmo não discutido em sala

## Funções Heurísticas

## Busca em ambientes complexos
### Algoritmo desenvolvido de busca em ambientes complexos

## Expansão do uso de algoritmos de busca

## Algoritmos genéticos.
### Exemplo de uso de algoritmos geneticos diferentes

## Uso de algoritmos de busca em IA

## Conclusão

## Referências

> [1] RUSSELL, Stuart; NORVIG, Peter. *Inteligência Artificial: Uma Abordagem Moderna* – 3ª edição.  
> [2] OPENAI. Assistente Virtual ChatGPT. Respostas geradas com base em inteligência artificial. Disponível em: https://openai.com. Acesso em: 24 dez. 2024.