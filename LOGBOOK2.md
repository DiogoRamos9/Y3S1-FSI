
# Trabalho realizado nas Semanas #2 e #3

## Identificação

- CVE-2024-8868
- O ataque pode ser realizado remotamente e não requer autenticação prévia, o que aumenta a sua gravidade
- Categoria: SQL Injection
- Sistemas afetados: "Code-projects Crud Operation System 1.0"

## Catalogação

- Data da publicação: 15-09-2024
- Descrição do Report: Problemas no arquivo savedata.php, que estava suscetível a injeções de SQL devido ao mau uso do parâmetro sname
- Local do Report: Plataformas como o VulDB e DEC Solutions Group, foram essenciais para os utilizadores saberem da gravidade da falha
- Nivel de gravidade: 7,3 de acordo com [CVE](https://www.cve.org/CVERecord?id=CVE-2024-8868)

## Exploit

- Tipo: SQL Injection
- Descrição: Modificar/extrair informações do bancos de dados
- Automação: Apps como SQLMap são capazes de injetar malware em ficheiros vulneráveis do sistema
- Metasploit: Não há relatos específicos ainda

## Ataques

- Potencial: Muito alto, uma vez que, a complexidade do ataque é muito baixa
- Consequências: Roubo de dados, comprometimento dos sistemas
- Ataques específicos ainda não foram encontrados/reportados em nenhum forum

