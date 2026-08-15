# Esboço do trabalho — Sistemas Operacionais, Processos, Threads e Assembly

**Disciplina:** Arquitetura de Sistemas Computacionais
**Professor:** [nome do professor]
**Data:** 15 de agosto de 2026

**Grupo:** Celso Pio das Chagas · Luiz Henrique [sobrenome] · Kauan Leal [sobrenome] ·
Matheus [sobrenome] · Matheus [sobrenome] (Roxo)

---

## Como organizamos o trabalho

Dividimos o relatório pelas quatro partes do enunciado, com um responsável por parte.
A regra que combinamos é que cada um não só escreve o seu trecho, mas precisa conseguir
explicar o tema para o resto do grupo depois — a ideia é que ninguém entregue um
pedaço que não saiba defender.

| Parte | Tema | Responsável |
|---|---|---|
| 1 | Tipos de sistemas operacionais | Luiz Henrique |
| 2 | Chamadas de sistema | Celso |
| 3 (a) | Comparação entre processos e threads | Kauan Leal |
| 3 (b) | Concorrência: condições de disputa e mutex | Matheus |
| 4 | Do código C ao Assembly | Celso |
| — | Montagem final, padronização e fontes consultadas | Matheus (Roxo) |

Como material de apoio principal estamos usando o livro do professor Carlos Maziero,
*Sistemas Operacionais: Conceitos e Mecanismos* (UFPR), que cobre quase tudo o que o
enunciado pede. Para os detalhes que dependem de arquitetura específica (registradores,
por exemplo) recorremos às páginas de manual do Linux, porque o livro é propositalmente
neutro nesse ponto.

## Parte 1 — Tipos de sistemas operacionais

Vamos montar a tabela comparativa pedida, com uma linha para cada tipo (lote, tempo
compartilhado, monolítico e microkernel) e colunas de definição, duas características,
exemplo de aplicação e um SO relacionado.

Um ponto que pretendemos deixar explícito num parágrafo curto depois da tabela: esses
quatro tipos não estão no mesmo eixo de classificação. Lote e tempo compartilhado
dizem respeito a *como as tarefas são submetidas e escalonadas*; monolítico e
microkernel dizem respeito a *onde o código do sistema roda*. Linux, por exemplo, é
monolítico e de tempo compartilhado ao mesmo tempo, o que só é contraditório se a
gente tratar os quatro como alternativas excludentes.

Base de leitura: capítulos "Conceitos básicos" (categorias e histórico) e "Arquiteturas
de SOs" do Maziero.

## Parte 2 — Chamadas de sistema

A seção começa explicando o que é uma chamada de sistema e por que um programa não
consegue simplesmente acessar o hardware por conta própria. Estamos organizando a
justificativa em três motivos:

- **Abstração.** Historicamente se escrevia direto no hardware, o que prendia o
  programa a uma máquina específica. Uma camada intermediária permite escrever código
  que roda em hardwares diferentes.
- **Gerência de recursos.** Com vários programas disputando os mesmos recursos, é
  preciso alguém arbitrando esse acesso.
- **Proteção.** A partir do momento em que os recursos são compartilhados, isolar um
  programa do outro deixa de ser opcional.

Vale registrar que quem de fato impede o acesso direto é o hardware, não uma convenção
do sistema operacional: os níveis de privilégio da CPU e a unidade de gerência de
memória. O núcleo é a abstração construída em cima desse mecanismo.

Também vamos incluir uma descrição passo a passo do caminho de uma chamada, desde o
programa em modo usuário até o retorno, passando pela troca de modo, pela consulta à
tabela de chamadas do núcleo e pela volta. Um detalhe que queremos deixar claro é a
diferença entre troca de modo e troca de contexto: toda chamada de sistema troca o modo
de execução, mas só algumas provocam uma troca de contexto completa, quando a chamada
bloqueia e o núcleo coloca outra tarefa para rodar.

As quatro chamadas escolhidas, uma por categoria:

| Categoria | Chamada | Situação |
|---|---|---|
| Arquivos | `write` | definida |
| Processos | `fork` | definida |
| Memória | `mmap` (provável) | a confirmar |
| Comunicação / informações | `socket` (provável) | a confirmar |

Para cada uma entra finalidade, o que recebe, o que retorna e um exemplo de uso.

A diferença entre chamada de sistema e função de biblioteca fecha a seção, usando o
exemplo do próprio enunciado: `printf` é função de biblioteca, roda em modo usuário e
faz *buffering*; quando o buffer é descarregado, ela chama `write`, que é a chamada de
sistema que efetivamente atravessa para o núcleo.

Base de leitura: capítulo "Estrutura de um SO", seção "Chamadas de sistema", mais as
seções sobre níveis de privilégio e interrupções. Para o trecho de registradores,
`man 2 syscall`.

**Andamento:** leitura e anotações em curso. As duas primeiras chamadas estão fechadas;
falta decidir as de memória e comunicação.

## Parte 3 — Processos e threads

### (a) Comparação

Tabela com as seis dimensões pedidas pelo enunciado — memória, custo de criação,
compartilhamento de dados, comunicação, isolamento de falhas e sincronização — seguida
das duas perguntas de fechamento: quando faz mais sentido usar um processo e quando faz
mais sentido usar uma thread.

Base de leitura: capítulo "Implementação de tarefas", que tem uma seção específica de
uso de processos versus threads.

### (b) Concorrência

Explicação de condição de corrida (o Maziero usa o termo "condições de disputa") e do
papel do mutex como mecanismo de exclusão mútua, mais um exemplo de software real que
usa múltiplos processos ou múltiplas threads.

Base de leitura: capítulos "Coordenação entre tarefas" e "Mecanismos de coordenação".

## Parte 4 — Do código C ao Assembly

O programa escolhido é uma função de aproximadamente doze linhas chamada `send_all`,
retirada de um servidor HTTP em C que um dos integrantes está escrevendo como projeto
de estudo. Ela recebe um descritor, um ponteiro para os dados e um tamanho, e repete a
escrita até que todos os bytes tenham saído, porque uma escrita pode ser parcial.

Escolhemos essa função por dois motivos. Primeiro, ela atende de uma vez quase todos os
elementos sugeridos pelo enunciado: tem uma função, um laço de repetição, uma estrutura
condicional e aritmética sobre ponteiro. Segundo, é código escrito pelo próprio grupo,
então conseguimos explicar cada decisão dela, o que não aconteceria com um exemplo
genérico copiado de tutorial.

O plano é compilar com `-O0` e `-O2`, selecionar entre três e oito instruções do trecho
correspondente ao laço, e explicar o que cada uma faz, quais registradores aparecem e
onde as duas versões divergem. A expectativa é que a diferença mais visível esteja no
tratamento das variáveis locais: sem otimização elas tendem a ir e voltar da pilha a
cada iteração, enquanto com otimização o compilador deve mantê-las em registradores.

Arquitetura, sistema operacional e compilador serão registrados no relatório, conforme
o enunciado pede. Ainda estamos decidindo entre rodar em x86-64 sobre Linux ou usar a
máquina que temos à mão, que é ARM64 sobre macOS — a escolha muda os registradores que
aparecem no Assembly, então precisa estar declarada com clareza.

**Andamento:** função escolhida e compilando. Falta gerar e analisar os dois arquivos
de Assembly.

## Fontes consultadas (preliminar)

MAZIERO, Carlos A. **Sistemas Operacionais: Conceitos e Mecanismos**. Curitiba:
DINF – UFPR, 2019. ISBN 978-85-7335-340-2. Disponível em:
<https://wiki.inf.ufpr.br/maziero/doku.php?id=socm:start>. Acesso em: 15 ago. 2026.

*The Linux man-pages project.* `syscall(2)`, `write(2)`, `fork(2)`. Disponível em:
<https://man7.org/linux/man-pages/>. Acesso em: 15 ago. 2026.

A lista será consolidada na versão final, junto com as fontes usadas pelas partes 1 e 3.

## Pontos ainda em aberto

- Definição das chamadas de sistema de memória e de comunicação (Parte 2).
- Escolha da arquitetura e do compilador para os testes da Parte 4.
- Exemplo de software concorrente a ser citado na Parte 3 (b).
