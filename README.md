# Exercício: Sistemas Operacionais, Processos, Threads e Assembly

- **Público-alvo:** alunos de Arquitetura de Software
- **Modalidade:** grupos de 2 a 4 alunos
- **Carga horária:** 3 horas
- **Entrega:** relatório técnico curto

## Objetivos

- Conhecer diferentes tipos de sistemas operacionais.
- Compreender chamadas de sistema (system calls).
- Diferenciar processos e threads.
- Observar como um código em C é transformado em instruções Assembly.

## Parte 1 — Tipos de sistemas operacionais

Pesquise pelo menos quatro tipos de sistemas operacionais, escolhendo entre:

- Sistemas em lote (batch).
- Sistemas de tempo compartilhado.
- Sistemas Monolíticos.
- Sistemas Microkernel.

Para cada tipo, apresente:

- Uma definição.
- Duas características.
- Um exemplo de aplicação.
- Um sistema operacional relacionado.

Organize os resultados em uma tabela comparativa.

## Parte 2 — Chamadas de sistema

Explique o que é uma chamada de sistema e por que os programas precisam delas para
acessar recursos controlados pelo sistema operacional.

Escolha e pesquise quatro chamadas de sistema, sendo uma de cada categoria:

| Categoria                  | Exemplos                    |
| -------------------------- | --------------------------- |
| Arquivos                   | open, read, write, close    |
| Processos                  | fork, execve, wait, exit    |
| Memória                    | mmap, brk                   |
| Comunicação ou informações | pipe, socket, getpid, uname |

Para cada chamada selecionada, informe:

- Sua finalidade.
- O que ela recebe como entrada.
- O que retorna.
- Um exemplo de utilização.

Explique também a diferença entre uma chamada de sistema e uma função de biblioteca.
Por exemplo, `printf()` é uma função da biblioteca C que pode utilizar internamente a
chamada de sistema `write()`.

## Parte 3 — Processos e threads

Produza uma comparação entre processos e threads considerando:

- Memória.
- Custo de criação.
- Compartilhamento de dados.
- Comunicação.
- Isolamento de falhas.
- Sincronização.

Depois, responda:

- Quando é mais adequado utilizar um processo?
- Quando é mais adequado utilizar uma thread?
- O que é uma condição de corrida?
- Para que serve um mutex?

Apresente um exemplo de software que utilize múltiplos processos ou múltiplas threads.

## Parte 4 — Do código C ao Assembly

O grupo deverá escolher ou criar um pequeno, de 10 linhas no máximo em C. O código pode
conter, por exemplo:

- Uma operação matemática.
- Uma estrutura condicional.
- Um laço de repetição.
- Uma função.
- Uma operação sobre um vetor.
- Uma combinação desses elementos.

O programa deve ter aproximadamente 5 a 20 linhas, desconsiderando comentários e linhas
em branco.

### Compilação

Salve o programa em um arquivo, por exemplo, `programa.c`.

Gere o código Assembly sem otimização:

```
gcc -O0 -S programa.c -o programa_O0.s
```

Gere também uma versão com otimização:

```
gcc -O2 -S programa.c -o programa_O2.s
```

Em computadores com arquitetura x86-64, é possível solicitar a sintaxe Intel:

```
gcc -O0 -S -masm=intel programa.c -o programa_O0.s
```

O grupo também poderá utilizar outro compilador, ou outra arquitetura de processador,
desde que registre essas informações no relatório.

### Análise

Selecione de três a oito instruções Assembly produzidas pelo compilador e explique:

- Qual parte do código C está relacionada a essas instruções.
- O que cada instrução realiza.
- Quais registradores aparecem no trecho.
- Se existem diferenças entre as versões `-O0` e `-O2`.
- Qual foi a arquitetura, o sistema operacional e o compilador utilizados.

Não é necessário explicar todo o arquivo Assembly. O objetivo é identificar uma relação
clara entre um pequeno trecho do código C e as instruções geradas.

O Assembly pode variar conforme o processador, o sistema operacional, o compilador e o
nível de otimização.

## Organização sugerida das 3 horas

| Tempo      | Atividade                                    |
| ---------- | -------------------------------------------- |
| 45 minutos | Pesquisa sobre tipos de sistemas operacionais |
| 40 minutos | Pesquisa sobre chamadas de sistema            |
| 35 minutos | Comparação entre processos e threads          |
| 45 minutos | Compilação e análise do código C em Assembly  |
| 15 minutos | Organização e revisão da entrega              |

## Produto final

Entregar um relatório de 3 a 5 páginas contendo:

1. Tabela dos tipos de sistemas operacionais.
2. Explicação das quatro chamadas de sistema.
3. Comparação entre processos e threads.
4. Código C escolhido pelo grupo.
5. Trecho do Assembly gerado.
6. Explicação das instruções selecionadas.
7. Comparação entre as versões com e sem otimização.
8. Fontes consultadas.
