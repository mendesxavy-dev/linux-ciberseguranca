# Mini-Relatório Técnico - Análise de Vulnerabilidades com Lynis

## Informações do Curso
* **Curso:** Reskilling – Linux e Cibersegurança
* **Módulo:** Linux e Cibersegurança  
* **Formador:** Péricles Borges
* **Formando:** Paulo Vieira

---

## 1. Métrica Inicial de Segurança
* **Hardening Score:** 63
* **Warnings Encontrados:** 1
* **Suggestions Encontradas:** 50

---

## 2. Análise e Medidas Corretivas (Suggestions)

### Vulnerabilidade 1: Autenticação (`AUTH-9282`)
* **Descrição/Problema:** Existência de contas de utilizador com palavra-passe ativa sem data de expiração da conta definida (`Account expires: never`).
* **Medida Corretiva Proposta:** Estabelecer datas de expiração programadas para contas temporárias ou de terceiros através do comando `chage -E YYYY-MM-DD <utilizador>` e configurar o parâmetro `INACTIVE` em `/etc/default/useradd` para desativar automaticamente contas inativas.

### Vulnerabilidade 2: Ficheiros do Sistema (`FILE-6310`)
* **Descrição/Problema:** O diretório `/home` (assim como o `/tmp` e `/var`) não está numa partição isolada. Se um utilizador ou processo preencher o espaço total em disco, pode causar a falha completa de todo o sistema operativo.  
* **Medida Corretiva Proposta:** Configurar o esquema de partições durante a instalação do sistema (ou num ambiente de produção) de forma a alocar partições/volumes LVM dedicados e independentes para `/home`, `/tmp` e `/var`, garantindo a disponibilidade do sistema mesmo que uma partição fique cheia.

![sudo-lynis](imagens/sudo-lynis.png)

---

## 3. Excerto do Relatório Lynis

```text
================================================================================

  -[ Lynis 3.0.9 Results ]-

  Warnings (1):
  ----------------------------
  ! Found one or more vulnerable packages. [PKGS-7392] 
      https://cisofy.com/lynis/controls/PKGS-7392/

  Suggestions (50):
  ----------------------------
  * Install a PAM module for password strength testing like pam_cracklib or pam_passwdqc [AUTH-9262] 
      https://cisofy.com/lynis/controls/AUTH-9262/

  * When possible set expire dates for all password protected accounts [AUTH-9282] 
      https://cisofy.com/lynis/controls/AUTH-9282/

  * To decrease the impact of a full /home file system, place /home on a separate partition [FILE-6310] 
      https://cisofy.com/lynis/controls/FILE-6310/

================================================================================