# Organização do grupo

O que o professor pediu está no [`README.md`](../README.md), transcrito 1:1 do
`Exercício.docx`. Este arquivo é só a organização interna do time.

## Divisão

| Parte | Tema                                 | Responsável   |
| ----- | ------------------------------------ | ------------- |
| 1     | Tipos de sistemas operacionais       | Luiz Henrique |
| 2     | Chamadas de sistema                  | Celso         |
| 3a    | Processos vs. threads (tabela)       | Kauan Leal    |
| 3b    | Concorrência (condição de corrida, mutex) | Matheus  |
| 4     | Do código C ao Assembly              | Celso         |
| —     | sem tema definido                    | Matheus Roxo  |

Modelo de trabalho: cada um domina seu tema e **ensina para o resto do time** depois.

## Em aberto

- [ ] **Tema do Matheus Roxo.** Candidato natural: assumir a Parte 2 junto com o Celso,
      ou ficar responsável pela seção "Fontes consultadas" + revisão e formatação final.
- [ ] **"Fontes consultadas"** é item obrigatório do produto final e não tem dono.
- [ ] **Arquitetura dos experimentos.** Decidir entre:
      - container `linux/amd64` — alinha com `rax`/`rdi`, dá acesso a `strace` e ao `gcc` real;
      - ARM64 / macOS / Apple clang nativo — permitido pelo enunciado desde que registrado,
        mas usa `x0`–`x8` e `svc #0`, e não tem `strace`.
- [ ] **Como citar o `http-server-c`.** O servidor HTTP em C serve de base para os
      exemplos das Partes 2, 3b e 4, mas o repositório é privado — decidir se os trechos
      usados são copiados para `experimentos/` (relatório autocontido) ou se o repo é aberto.

## Nota sobre o enunciado

A Parte 4 se contradiz: diz "um pequeno, de 10 linhas no máximo em C" e, logo depois,
"aproximadamente 5 a 20 linhas". Escrevendo ~10 linhas, as duas leituras são atendidas.
