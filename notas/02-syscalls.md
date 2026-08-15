# Parte 2 — Chamadas de sistema (notas de estudo)

Estado: **em construção**. Depende de [`00-mapa-de-leitura.md`](00-mapa-de-leitura.md)
— ler *O conceito de tarefa* e *Implementação de tarefas* antes de fechar esta nota.

## Já consolidado

### Processo

Um processo é duas coisas ao mesmo tempo:

- um **espaço de endereçamento** na memória (pilha, heap, dados, código);
- um **contexto de registradores** na CPU.

Existe apenas um conjunto de registradores por núcleo. Trocar de processo, portanto,
significa salvar os registradores atuais no PCB e carregar os do próximo.

### Quem realmente impede o acesso direto ao hardware

O **hardware**, não o núcleo por convenção: os modos de execução da CPU e a MMU. O
núcleo é a abstração construída por cima desse mecanismo — ele não "pede educadamente"
que os programas não toquem no disco, ele opera num modo privilegiado que o programa
de usuário não consegue alcançar sozinho.

Consequência: a chamada de sistema não é uma chamada de função comum com outro nome.
É o único caminho legítimo para atravessar essa fronteira.

### ABI x86-64/Linux (fonte: `man 2 syscall`, **não** o Maziero)

- `rax` é um registrador de uso geral. Por **convenção da ABI** — não por característica
  física — ele carrega o número da chamada na entrada e o resultado na saída.
- A convenção de syscall **não é** a convenção de função C: o 4º argumento vai em `r10`,
  não em `rcx`, porque a instrução `syscall` destrói `rcx` e `r11`.
- A tabela de syscalls é um vetor de ponteiros para função; `rax` é o índice.

### `errno`

É invenção da glibc. O núcleo devolve um negativo pequeno em `rax` (`-9`, `-14`, …);
o *wrapper* da biblioteca converte isso em retorno `-1` e preenche `errno`.

### `printf` vs. `write`

`printf` é função de biblioteca: roda em modo usuário, formata a string e faz
*buffering*. Só quando o buffer é descarregado é que ela chama `write`, que é a
chamada de sistema — essa sim atravessa para o núcleo e escreve bytes num descritor
de arquivo. É o gancho que o próprio enunciado sugere.

### `fork`

Retorna **duas vezes**: o PID do filho no processo pai, `0` no filho, `-1` em erro.

## Ainda aberto

- [ ] Caminho completo de uma chamada, do processo até o retorno — passo a passo.
- [ ] Como exatamente o contexto é salvo e restaurado nesse trajeto.
- [ ] Onde a tabela de syscalls entra no caminho, concretamente.

## As quatro chamadas escolhidas

Uma de cada categoria exigida pelo enunciado. Para cada uma: finalidade, entrada,
retorno, exemplo.

| Categoria                  | Chamada    | Status |
| -------------------------- | ---------- | ------ |
| Arquivos                   | `write`    | ☐      |
| Processos                  | `fork`     | ☐      |
| Memória                    | a definir  | ☐      |
| Comunicação ou informações | a definir  | ☐      |
