Para todas as questões, compile-as com o gcc e execute-as via terminal.

1. Crie um "Olá mundo!" em C.

```c
#include <stdio.h>

int main(int argc, char const *argv[]) {
  printf("Hello world!!\n");
  return 0;
 }
```
2. Crie um código em C que pergunta ao usuário o seu nome, e imprime no terminal "Ola " e o nome do usuário. Por exemplo, considerando que o código criado recebeu o nome de 'ola_usuario_1':

```bash
$ ./ola_usuario_1
$ Digite o seu nome: Eu
$ Ola Eu
```

```c {}
#include <stdio.h>
#define LIMITE 100

int main(int argc, char const *argv[]) {
  char nome[LIMITE];
  printf("Digite o seu nome: ");
  scanf("%[^\n]%*c",nome);
  printf("Ola %s\n", nome);
  return 0;
}
```

3. Apresente os comportamentos do código anterior nos seguintes casos:

(a) Se o usuário insere mais de um nome.
```bash
$ ./ola_usuario_1
$ Digite o seu nome: Eu Mesmo
```

```bash
Saida : Ola Eu mesmo
```
(b) Se o usuário insere mais de um nome entre aspas duplas. Por exemplo:
```bash
$ ./ola_usuario_1
$ Digite o seu nome: "Eu Mesmo"
```

```bash
Saida : Ola "Eu mesmo"
```

(c) Se é usado um pipe. Por exemplo:
```bash
$ echo Eu | ./ola_usuario_1
```

```bash
Saida : Digite o seu nome: Ola Eu
```

(d) Se é usado um pipe com mais de um nome. Por exemplo:
```bash
$ echo Eu Mesmo | ./ola_usuario_1
```
```bash
Saida : Digite o seu nome: Ola Eu Mesmo
```

(e) Se é usado um pipe com mais de um nome entre aspas duplas. Por exemplo:
```bash
$ echo "Eu Mesmo" | ./ola_usuario_1
```
```bash
Saida : Digite o seu nome: Ola Eu Mesmo
```

(f) Se é usado o redirecionamento de arquivo. Por exemplo:
```bash
$ echo Ola mundo cruel! > ola.txt
$ ./ola_usuario_1 < ola.txt
```

```bash
Saida : Digite o seu nome: Ola Ola mundo cruel!
```

4. Crie um código em C que recebe o nome do usuário como um argumento de entrada (usando as variáveis argc e \*argv[]), e imprime no terminal "Ola " e o nome do usuário. Por exemplo, considerando que o código criado recebeu o nome de 'ola_usuario_2':

```bash
$ ./ola_usuario_2 Eu
$ Ola Eu
```

```c{}
#include <stdio.h>

int main(int argc, char const *argv[]) {
  printf("Ola %s\n", argv[1]);
  return 0;
}
```

5. Apresente os comportamentos do código anterior nos seguintes casos:

(a) Se o usuário insere mais de um nome.
```bash
$ ./ola_usuario_2 Eu Mesmo
```

```bash
Saida : Ola Eu
```

(b) Se o usuário insere mais de um nome entre aspas duplas. Por exemplo:
```bash
$ ./ola_usuario_2 "Eu Mesmo"
```

```bash
Saida : Ola Eu Mesmo
```

(c) Se é usado um pipe. Por exemplo:
```bash
$ echo Eu | ./ola_usuario_2
```

```bash
Saida : Ola (null)
```
(d) Se é usado um pipe com mais de um nome. Por exemplo:
```bash
$ echo Eu Mesmo | ./ola_usuario_2
```

```bash
Saida : Ola (null)
```

(e) Se é usado um pipe com mais de um nome entre aspas duplas. Por exemplo:
```bash
$ echo Eu Mesmo | ./ola_usuario_2
```

```bash
Saida : Ola (null)
```

(f) Se é usado o redirecionamento de arquivo. Por exemplo:
```bash
$ echo Ola mundo cruel! > ola.txt
$ ./ola_usuario_2 < ola.txt
```

```bash
Saida : Ola (null)
```

6. Crie um código em C que faz o mesmo que o código da questão 4, e em seguida imprime no terminal quantos valores de entrada foram fornecidos pelo usuário. Por exemplo, considerando que o código criado recebeu o nome de 'ola_usuario_3':

```bash
$ ./ola_usuario_3 Eu
$ Ola Eu
$ Numero de entradas = 2
```

```c
  #include <stdio.h>

  int main(int argc, char const *argv[]) {
    printf("Ola %s\n", argv[1]);
    printf("Número de entradas %d\n", argc);
    return 0;
  }

```
7. Crie um código em C que imprime todos os argumentos de entrada fornecidos pelo usuário. Por exemplo, considerando que o código criado recebeu o nome de 'ola_argumentos':

```bash
$ ./ola_argumentos Eu Mesmo e Minha Pessoa
$ Argumentos: Eu Mesmo e Minha Pessoa
```
```c
#include <stdio.h>

int main(int argc, char const *argv[]) {
  printf("Número de entradas %d\n", argc);
  for (int i = 1; i < argc; i++) {
    printf("Argumento número %d - %s\n",i, argv[i]);
  }
  return 0;
}

```

8. Crie uma função que retorna a quantidade de caracteres em uma string, usando o seguinte protótipo:
`int Num_Caracs(char *string);` Salve-a em um arquivo separado chamado 'num_caracs.c'. Salve o protótipo em um arquivo chamado 'num_caracs.h'. Compile 'num_caracs.c' para gerar o objeto 'num_caracs.o'.

Num_caracs.c
```C
#include <stdio.h>
#include <string.h>
#include "num_caracs.h"

int Num_Caracs(char *string){
  return strlen(string);

}
```
Num-caracs.h
```C{}
#ifndef NUM_CARACS__H
#define NUM_CARACS__H

int Num_Caracs(char *string);

#endif
}
```


9. Re-utilize o objeto criado na questão 8 para criar um código que imprime cada argumento de entrada e a quantidade de caracteres de cada um desses argumentos. Por exemplo, considerando que o código criado recebeu o nome de 'ola_num_caracs_1':

```bash
$ ./ola_num_caracs_1 Eu Mesmo
$ Argumento: ./ola_num_caracs_1 / Numero de caracteres: 18
$ Argumento: Eu / Numero de caracteres: 2
$ Argumento: Mesmo / Numero de caracteres: 5
```

```c
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[]) {
  printf("Número de entradas %d\n", argc);
  for (int i = 0; i < argc; i++) {
    printf("Argumento número %d - %s - Numero de caracteres %d\n",i, argv[i],Num_Caracs(argv[i]));
  }
  return 0;
}

```

10. Crie um Makefile para a questão anterior.

```bash
all:  
  gcc -o ola_num_caracs_1 num_caracs.c ola_num_caracs_1.c  

```


11. Re-utilize o objeto criado na questão 8 para criar um código que imprime o total de caracteres nos argumentos de entrada. Por exemplo, considerando que o código criado recebeu o nome de 'ola_num_caracs_2':

```bash
$ ./ola_num_caracs_2 Eu Mesmo
$ Total de caracteres de entrada: 25
```

```c
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[]) {
  printf("Número de entradas %d\n", argc);
  int numTotal =0;
  for (int i = 0; i < argc; i++) {
    numTotal = numTotal + Num_Caracs(argv[i]);
  }
  printf("Numero de caracteres %d\n",numTotal);
  return 0;
}

```

12. Crie um Makefile para a questão anterior.


```bash
all:  
  gcc -o ola_num_caracs_2 num_caracs.c total_caracs.c  

```
