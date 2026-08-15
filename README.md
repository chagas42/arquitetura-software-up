# Arquitetura de Software — Trabalho de SO, Processos, Threads e Assembly

Repositório de estudo e produção do trabalho. O enunciado do professor está
transcrito em [`enunciado.md`](enunciado.md).

## Divisão do grupo

| Parte  | Tema                                   | Responsável   |
| ------ | -------------------------------------- | ------------- |
| 1      | Tipos de sistemas operacionais         | Luiz Henrique |
| 2      | Chamadas de sistema                    | Celso         |
| 3a     | Processos vs. threads (tabela)         | Kauan Leal    |
| 3b     | Concorrência (race condition, mutex)   | Matheus       |
| 4      | Do código C ao Assembly                | Celso         |
| —      | sem tema definido                      | Matheus Roxo  |

Modelo de trabalho: cada um domina seu tema e **ensina para o resto do time** depois.

## Pendências abertas

- [ ] **Tamanho do grupo.** O enunciado pede grupos de 2 a 4 alunos; somos 5.
      Confirmar com o professor antes da entrega.
- [ ] **Tema do Matheus Roxo.** Candidato natural: assumir a Parte 2 junto com o Celso,
      ou ficar responsável pela seção "Fontes consultadas" + revisão/formatação final.
- [ ] **Seção "Fontes consultadas"** é obrigatória no produto final e não tem dono.
- [ ] **Arquitetura dos experimentos.** Decidir entre:
      - container `linux/amd64` (alinha com `rax`/`rdi`, dá acesso a `strace` e ao `gcc` real);
      - ARM64 / macOS / Apple clang nativo (permitido pelo enunciado, desde que registrado,
        mas usa `x0`–`x8` e `svc #0`, e não tem `strace`).

## Estrutura

```
notas/          anotações de estudo (leitura do Maziero + man pages)
experimentos/   código e saídas reais (strace, .s gerados)
relatorio/      texto que vai para a entrega
```

## Material de apoio

- MAZIERO, Carlos A. *Sistemas Operacionais: Conceitos e Mecanismos*. UFPR.
  <https://wiki.inf.ufpr.br/maziero/doku.php?id=socm:start>
  (referenciar por **nome de capítulo**, não por página — a numeração muda entre versões do PDF)
- `man 2 syscall` — para os detalhes de ABI x86-64/Linux, que **não** estão no Maziero.
