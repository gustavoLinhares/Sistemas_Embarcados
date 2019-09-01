1. Crie um arquivo com nome _teste1.txt_, e escreva nele o texto "Número do arquivo = 1". Repita o procedimento para os arquivos _teste2.txt_, _teste3.txt_, ..., _teste100.txt_, escrevendo o texto correspondente para cada um deles ("Número do arquivo = 2", "Número do arquivo = 3", ..., "Número do arquivo = 100").

Para fazer um executável usar chmod +x fileName


```bash
#!/bin/bash
for i in {1..10}
do
  echo "Número do arquivo = ${i}" > "teste${i}.txt"
done
```

2. Faça um script chamado _cals.sh_ que apresente o calendário de vários meses indicados pelo usuário, usando o seguinte formato:

```bash
#!/bin/bash
echo $# argumentos passados
if [ $# -ge 1 ]; then
  aux=("$@")
  i=0
  j=$#
  while [[ j -gt 0 ]]; do
    cal -my "$((${aux[i]}))" "$((${aux[i+1]}))"
    j="$((j - 2))"
    i="$((i + 2))"
  done
fi

```

3. Utilizando a lógica do script anterior, descubra em que dia da semana caiu o seu aniversário nos últimos dez anos.

```bash
#!/bin/bash
echo "Digite o mes do seu aniversário:"
read mes
if [ $mes -ge 1 ]; then
  aux=2019
  j=10
  while [[ j -gt 0 ]]; do
    cal -my "$((mes))" "$((aux))"
    j="$((j - 1))"
    aux="$((aux - 1))"
  done
fi
```

4. Crie um arquivo _sites.txt_ com o seguinte conteúdo:

```
https://github.com/DiogoCaetanoGarcia/Sistemas_Embarcados/raw/master/Aulas/01_Linux%20b%C3%A1sico.pdf
https://github.com/DiogoCaetanoGarcia/Sistemas_Embarcados/raw/master/Aulas/01_Linux%20b%C3%A1sico_Shell_Script.pdf
https://github.com/DiogoCaetanoGarcia/Sistemas_Embarcados/raw/master/Aulas/01_Sistemas%20Embarcados%20-%20Aula%201%20-%20Introdu%C3%A7%C3%A3o.pdf
```

Estes são links para slides de 3 aulas desta dsciplina, um para cada linha do arquivo _sites.txt_. Faça um script que faz o download destes slides automaticamente, a partir do arquivo _sites.txt_. (DICA: use o comando wget.)

```bash
#!/bin/bash
filename='sites.txt'
n=1
while read line; do
 wget "$line"
 n=$((n+1))
done < $filename

```


5. Faça um script chamado _up.sh_ que sobe _N_ níveis na pasta onde você estiver, usando $1 como parâmetro de entrada. Por exemplo, se você estiver em **/home/aluno/Documents** e executar **./up.sh 2**, você automaticamente vai para a pasta **/home**.

Usa o ponto antes de executar o código . ./up.sh , caso contrário não funcionará

```bash
#!/bin/bash
echo $1 argumento1
for i in $(seq $1); do
  cd ..
done

```
