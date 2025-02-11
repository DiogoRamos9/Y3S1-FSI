## CTF WEEK4

**Objetivo** Explorar a forma como variáveis de ambiente afetam a execução de programas em sistemas Linux.


**Descrição da vulnerabilidade encontrada** Ao navegar pelo site percebemos que ao colocar **";"**
eramos redirecionados para uma páginas com as variáveis ambiente. Seguidamente percebemos que se à frente do **";"** colocássemos qualquer comando que usamos normalmente na shell, por exemplo ls -la, debaixo das variáveis ambiente aparecia todos os ficheiros do diretório e as permissões deles. Depois de algum tempo, percebemos que a vulnerabilidade seria certamente uma **command injection**.


Flag 1 -> flag{[CVE-2014-6271](https://nvd.nist.gov/vuln/detail/CVE-2014-6271)}



**Explorar a vulnerabilidade**

- Primeiro começamos por procurar onde estaria localizado o ficheiro da flag, e com vários **; ls -la**, localizámos o ficheiro flags.txt, nos diretórios /var/flag.

![](imgsweek4/ctf4comandoencontrar.PNG)

- Depois de perceber onde está of ficheiro flag.txt, executámos o comando **more** e somos redirecionados para uma página com o output do comando, ou seja a flag.

![](imgsweek4/CTF4.PNG)

**Flag encontrada** Flag 2 -> flag{HLwXGJUSz6C2pK2Gvs49cNGH2F52js}


![](imgsweek4/ctf4lfag.PNG)

---