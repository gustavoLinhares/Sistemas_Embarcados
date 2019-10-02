Para todas as questões, utilize as funções da biblioteca `stdio.h` de leitura e de escrita em arquivo (`fopen()`, `fclose()`, `fwrite()`, `fread()`, dentre outras). Compile os códigos com o gcc e execute-os via terminal.

Para abertura e fechamento de arquivos as seguintes funções foram utilizadas assim facilitando o desenvolvimento dos códigos
```c{}
FILE *abreArquivo (const char *tipo, const char *nomeArquivo){
  FILE *arquivo;
  arquivo = fopen(nomeArquivo,tipo);
  if(ferror(arquivo)){
      printf("Arquivo não pode ser aberto\n");
      return NULL;
  }
  else{
      return arquivo;
  }
}

void fechaArquivo (FILE *arquivo){
  fclose(arquivo);
  if(ferror(arquivo)){
    printf("Arquivo não pode ser fechado\n");
  }
  else{
    printf("Arquivo fechado com sucesso \n");
  }
}
```

1. Crie um código em C para escrever "Ola mundo!" em um arquivo chamado 'ola_mundo.txt'.

```c{}
#include <stdio.h>
#include <string.h>
FILE *abreArquivo (const char *tipo, const char *nomeArquivo);
void fechaArquivo (FILE *arquivo);

int main(int argc, char const *argv[]) {
    FILE *pf;
    char mensagem[] = "Ola mundo! \n";
    pf = abreArquivo("w","ola_mundo.txt");
    if (pf != NULL){
      printf("Arquivo Criado e mensagem esrita\n");
      fwrite(mensagem,sizeof(char),strlen(mensagem),pf);
    }
    fechaArquivo(pf);
    return 0;
}
```

2. Crie um código em C que pergunta ao usuário seu nome e sua idade, e escreve este conteúdo em um arquivo com o seu nome e extensão '.txt'. Por exemplo, considerando que o código criado recebeu o nome de 'ola_usuario_1':

```bash
$ ./ola_usuario_1
$ Digite o seu nome: Eu
$ Digite a sua idade: 30
$ cat Eu.txt
$ Nome: Eu
$ Idade: 30 anos
```

```c{}
#include <stdio.h>
#include <string.h>
#define MAX 50
FILE *abreArquivo (const char *tipo, const char *nomeArquivo);
void fechaArquivo (FILE *arquivo);

int main(int argc, char const *argv[]) {
    FILE *pf;
    char nome[MAX],nomeFile[MAX];
    int idade;

    printf("Digite seu nome: ");
    scanf("%s",nome);
    printf("Digite sua idade: ");
    scanf("%d", &idade);
    strcpy(nomeFile,nome);
    strcat(nomeFile, ".txt");
    pf = abreArquivo("w",nomeFile);
    if (pf != NULL){
      fprintf(pf, "nome:  %s\nidade: %d anos\n",nome,idade);
    }
    fechaArquivo(pf);
    return 0;
}

```

3. Crie um código em C que recebe o nome do usuário e e sua idade como argumentos de entrada (usando as variáveis `argc` e `*argv[]`), e escreve este conteúdo em um arquivo com o seu nome e extensão '.txt'. Por exemplo, considerando que o código criado recebeu o nome de 'ola_usuario_2':

```bash
$ ./ola_usuario_2 Eu 30
$ cat Eu.txt
$ Nome: Eu
$ Idade: 30 anos
```

```c{}
#include <stdio.h>
#include <string.h>
#define MAX 50
FILE *abreArquivo (const char *tipo, const char *nomeArquivo);
void fechaArquivo (FILE *arquivo);

int main(int argc, char const *argv[]) {
    FILE *pf;
    char nomeFile[MAX];
    int idade;
    strcpy(nomeFile,argv[1]);
    strcat(nomeFile, ".txt");
    pf = abreArquivo("w",nomeFile);
    if (pf != NULL){
      fprintf(pf, "nome: %s\nidade: %s anos\n",argv[1],argv[2]);
    }
    fechaArquivo(pf);
    return 0;
}


```

4. Crie uma função que retorna o tamanho de um arquivo, usando o seguinte protótipo: `int tam_arq_texto(char *nome_arquivo);` Salve esta função em um arquivo separado chamado 'bib_arqs.c'. Salve o protótipo em um arquivo chamado 'bib_arqs.h'. Compile 'bib_arqs.c' para gerar o objeto 'bib_arqs.o'.

```c{}
  // bib.arqs.h
int tam_arq_texto(char *nome_arquivo);  

```

```c{}
// bib.arqs.c
#include <stdio.h>
#include <string.h>
#include "bib.arqs.h"

int tam_arq_texto(char *nome_arquivo){
  FILE *pf;
  int tamanho;
  pf = abreArquivo("ab",nome_arquivo);
  if (pf != NULL) {
    fseek(pf,0,SEEK_END);
    tamanho = ftell(pf);
    fechaArquivo(pf);
    return tamanho;
  }
  else{
    return 0;
  }
}

```


5. Crie uma função que lê o conteúdo de um arquivo-texto e o guarda em uma string, usando o seguinte protótipo: `char* le_arq_texto(char *nome_arquivo);` Repare que o conteúdo do arquivo é armazenado em um vetor interno à função, e o endereço do vetor é retornado ao final. (Se você alocar este vetor dinamicamente, lembre-se de liberar a memória dele quando acabar o seu uso.) Salve esta função no mesmo arquivo da questão 4, chamado 'bib_arqs.c'. Salve o protótipo no arquivo 'bib_arqs.h'. Compile 'bib_arqs.c' novamente para gerar o objeto 'bib_arqs.o'.



6. Crie um código em C que copia a funcionalidade básica do comando `cat`: escrever o conteúdo de um arquivo-texto no terminal. Reaproveite as funções já criadas nas questões anteriores. Por exemplo, considerando que o código criado recebeu o nome de 'cat_falsificado':

```bash
$ echo Ola mundo cruel! Ola universo ingrato! > ola.txt
$ ./cat_falsificado ola.txt
$ Ola mundo cruel! Ola universo ingrato!
```

7. Crie um código em C que conta a ocorrência de uma palavra-chave em um arquivo-texto, e escreve o resultado no terminal. Reaproveite as funções já criadas nas questões anteriores. Por exemplo, considerando que o código criado recebeu o nome de 'busca_e_conta':

```bash
$ echo Ola mundo cruel! Ola universo ingrato! > ola.txt
$ ./busca_e_conta Ola ola.txt
$ 'Ola' ocorre 2 vezes no arquivo 'ola.txt'.
```
