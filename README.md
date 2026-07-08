# Linux Terminal Banner 🐧 - 05/2026

Script simples em Bash para personalizar o terminal Linux com um banner ASCII centralizado, utilizando FIGlet e Lolcat.

## Preview

<img width="1115" height="627" alt="terminal" src="https://github.com/user-attachments/assets/3dc91a29-c881-46a4-b8df-30e8e435905d" />

## Ferramentas

- Bash
- Linux/Ubuntu
- FIGlet
- Lolcat

## Instalação 

Execute os comandos abaixo para instalar as dependências:

```bash
sudo apt update
sudo apt install figlet lolcat
```

## Como personalizar

Antes de testar o banner, altere o nome e a frase que deseja exibir no terminal.

Para alterar o nome, modifique esta linha:

```bash
figlet -f slant "Seu nome" 
```

Exemplo: 

```bash
figlet -f slant "Rainer Sacks"
```

Para alterar a frase ou descrição, modifique esta linha:

```bash
ascii_box "Coloque o que quiser" 
```

Exemplo: 

```bash
ascii_box "Software Engineering"
```

## Testar antes de adicionar ao .bashrc

Depois de personalizar o nome e a frase, copie e cole o código abaixo diretamente no terminal para testar o banner antes de adicionar ao arquivo `.bashrc`:

```bash
clear

TERMWIDTH=$(tput cols)

ascii_box() {
    texto="$1"

    topo=""
    meio=""

    for (( i=0; i<${#texto}; i++ )); do
        char="${texto:$i:1}"

        if [[ "$char" == " " ]]; then
            topo="${topo}+ "
            meio="${meio}| "
        else
            topo="${topo}+-"
            meio="${meio}|${char}"
        fi
    done

    topo="${topo}+"
    meio="${meio}|"

    echo "$topo"
    echo "$meio"
    echo "$topo"
}

figlet -f slant "Seu nome" | while IFS= read -r line; do
    printf "%*s\n" $(((${#line} + TERMWIDTH) / 2)) "$line"
done | lolcat -a

echo ""

ascii_box "Coloque o que quiser" | while IFS= read -r line; do
    printf "%*s\n" $(((${#line} + TERMWIDTH) / 2)) "$line"
done | lolcat -a

echo ""
```

## Adicionar ao arquivo .bashrc

Depois de testar e confirmar que funcionou corretamente, abra o arquivo `.bashrc`:

```bash
nano ~/.bashrc
```

Cole apenas o código do banner no final do arquivo.

> Não cole os comandos de instalação dentro do `.bashrc`.

Depois, salve o arquivo:

```text
Ctrl + O
Enter
Ctrl + X
```

Aplique as alterações:

```bash
source ~/.bashrc
```

## Observação

Os comandos abaixo devem ser executados apenas uma vez no terminal:

```bash
sudo apt update
sudo apt install figlet lolcat
```

Eles servem apenas para instalar as dependências necessárias e não devem ser adicionados ao arquivo `.bashrc`.

## Resultado esperado
Sempre que o terminal for aberto, o banner personalizado será exibido automaticamente com o nome e a frase escolhidos.
