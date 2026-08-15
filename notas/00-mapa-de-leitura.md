# Mapa de leitura

## A ordem importa

A primeira tentativa de estudar a Parte 2 foi direto pelo capítulo de chamadas de
sistema, e travou em quatro pontos:

1. o caminho completo de uma syscall, do processo até o retorno;
2. o que é um registrador e como ele se relaciona com o processo;
3. o que é a tabela de syscalls;
4. contexto de execução e troca de contexto.

Os quatro dependem da mesma base. Uma chamada de sistema **é** uma troca de contexto
(usuário → núcleo → usuário). Sem entender o que é o contexto que está sendo trocado,
o capítulo de syscall vira decoreba.

Daí a ordem adotada:

| # | Capítulo do Maziero              | Por que antes                                                    | Status |
| - | -------------------------------- | ---------------------------------------------------------------- | ------ |
| 1 | *O conceito de tarefa*           | define o que é uma tarefa e o que compõe seu contexto             | ☐      |
| 2 | *Implementação de tarefas*       | PCB, salvamento/restauração de contexto, despachante              | ☐      |
| 3 | *Estrutura do sistema operacional* | modos de execução, interrupções, **chamadas de sistema**        | ☐      |

> Confirmar os nomes exatos dos capítulos contra o PDF na hora de citar — referenciar
> sempre por nome, nunca por número de página.

## Depois do Maziero

O livro é neutro em relação à arquitetura. Os detalhes concretos que aparecem na
Parte 2 — `rax`, `rdi`, a instrução `syscall`, `sys_call_table` — são **x86-64/Linux**
e a referência para eles é `man 2 syscall`, não o Maziero. Manter as duas fontes
separadas no relatório para não atribuir ao autor coisa que ele não escreveu.

## Método

Ler → explicar em voz alta sem olhar → escrever a nota → ser arguido. O que não
sobreviver à arguição volta para a leitura.
