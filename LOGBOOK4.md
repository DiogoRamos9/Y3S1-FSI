# Logbook 4

## Task 1

- Na task 1, resumidamente conseguimos perceber qual é o output e para que servem comandos como "env"/"printenv" (mostrar variáveis ambiente) e  "printenv PWD"/"env | grep PWD" (escolher varáveis ambiente específicas) e "export"/"unset" (manipular variáveis ambiente).

- **printenv:**

![](imgsweek4/task1printenv.PNG)

- **env:**

![](imgsweek4/task1env.PNG)

- **printenv PWD:**
![](imgsweek4/task1printenvpwd.PNG)

- **env | grep PWD:**
![](imgsweek4/task1envpwd.PNG)

- **export:**

![](imgsweek4/task1export.PNG)



## Task 2

**Program**
``` c
#include <unistd.h>

#include <stdio.h>

#include <stdlib.h>

extern char **environ;

void printenv()

{
  int i = 0;

  while (environ[i] != NULL) {

     printf("%s\n", environ[i]);

     i++;

  }

}

void main()

{
  pid_t childPid;

  switch(childPid = fork()) {

    case 0:  /* child process */

      // printenv();          

      exit(0);

    default:  /* parent process */

      printenv();       

      exit(0);
  }
}
```

- Compilamos o ficheiros duas vezes, alterando da segunda vez o printenv() para o processo pai,seguidamente salvamos o ficheiro .out em dois ficheiros diferentes, ou seja, basicamente guardamos as variáveis de ambiente.

- A conclusão final que se retira quando se usa o comando diff é que o output é o mesmo para os dois processos, ou seja, as variáveis ambiente para os dois processos (pai e filho), são exatamente as mesmas, quando criadas com o através do **fork()** .

**Terminal:**

![](imgsweek4/task2.PNG)


## Task 3

**Programa:**

``` c
#include <unistd.h>

extern char **environ;

int main()
{
  char *argv[2];

  argv[0] = "/usr/bin/env";
  argv[1] = NULL;

  execve("/usr/bin/env", argv, NULL);  

  return 0 ;
}
```

- O programa inicial não imprime qualquer output, uma vez que,a função **execve** começa um processo associado e associa-o a um **array** de variáveis ambiente,como o terceiro argumento da é NULL, o novo processo não contém variáveis ambiente.

- Ao trocar o terceiro argumento pelo array de variáveis ambiente do processo pai **(environ)**,
o programa passa a imprimir, as variáveis ambiente desse processo. Era de esperar, pois o programa herda automaticamente a varáveis ambiente.

**Programa alterado e Output**

![](imgsweek4/task3.PNG)

## Task 4

- Nesta tarefa, criamos um ficheiro system.c, compilamos e corremos, e a conclusão que se retira é que o output da função system() e execve() é o mesmo, as variáveis ambiente do processo pai. Era facilmente previsível, pois a função system() usa excl, e a função execl chama execve.

**Terminal**

![](imgsweek4/task4.PNG)


## Task 5

**Processo:**

![](imgsweek4/task5part1.PNG)

Depois de realizados todos os processos, as conclusões que conseguimos tirar são:

- A **variável** ambiente que nós criamos e o **Path** aparecem quando executado o programa.


- E **LD_Library_Path** não aparece nas variáveis ambiente, pois o sistema por motivos de segurança oculta, para prevenir possiveis ataques ao sistema.

**Output**

![](imgsweek4/task5part2.PNG)


## Task6

-Começamos por criar um ficheiro myls.c com este código, e torná lo um programa Set-UID e mudar o dono para a root. Quando executado, o programa faz basicamente a função do comando **ls**.


**Programa**

``` c
#include <stdio.h>
#include <stdlib.h>

int main(){
    system("ls");
    return 0;
}
```

-No mesmo diretório criamos um ficheiro fake.c, para simular um ficheiro malicioso. 

``` c
#include <stdio.h>
#include <stdlib.h>

int main() {
    printf("AI AI AI ENTROU!!!\n");
    system("chmod 777 ~/Downloads/category-software/Environment_Variable_and_SetUID/Labsetup/important");
    return 0;
}
```

-Depois de executarmos este programa, com o comando ls -l vemos que as permissões mudaram, ou seja, se fosse um ficheiro malicioso tinha sido bem sucedido o ataque.

-O único problema são as contramedidas que existem, que acabam por chamar /bin/dash. Tivemos portanto que mudar o apontador para /bin/zsh com o comando que nos forneceram.(**sudo ln -sf /bin/zsh /bin/sh**).

**Passos realizados e output**

![](imgsweek4/task6comp.PNG)

![](imgsweek4/task6result.PNG)


## Task 8

- Começamos por compilar o programa, seguidamente mudamos o seu owner para root, e fizemos do catall um programa Set-Uid.

![](imgsweek4/task8inicio.PNG)

- Criámos um ficheiro critico.txt,depois mudámos as permissões do ficheiro para que este não pudesse ser lido pelo user normal **seed**.

![](imgsweek4/task8critico.PNG)

- Depois executamos o programa **catall** com o comando para remover o ficheiro critico criada. E como podemos ver na imagem, o ficheiro foi eliminado.

![](imgsweek4/task8exploit.PNG)


**Conclusão:**

Conseguimos perceber a clara insegurança do uso da função system() em programas com permissões muito elevadas no sistema. Como se observa pelas imagens ao usarmos o programa **catall** que invoca a função system(), e passando um comando para remover um ficheiro do sistema, sem nenhuma dificuldade este programa elimina o ficheiro critico.txt que não tem permissões. Portanto deve existir um grande cuidado quando se usa qualquer programa que invoca a função system().

---

