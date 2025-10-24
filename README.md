# Relatório de Teste — Ataque de Força Bruta (Medusa / Metasploitable2)

---

**Autor:** Jodi Vockt
**Curso / Evento:** DIO — Curso de Cybersecurity
**Data do teste:** 24/10/2025
**Ambiente:** Laboratório controlado (VMs Kali Linux + Metasploitable2 em VirtualBox, rede host-only)
**Observações:** Teste realizado em ambiente controlado com autorização.

---

## Sumário

1. [Introdução](#introdução)
2. [Objetivos](#objetivos)
3. [Escopo e Restrições](#escopo-e-restrições)
4. [Arquitetura do Ambiente de Teste](#arquitetura-do-ambiente-de-teste)
5. [Metodologia](#metodologia)
6. [Ferramentas e Wordlists](#ferramentas-e-wordlists)
7. [Execução dos Testes (passo a passo)](#execução-dos-testes-passo-a-passo)
8. [Recomendações e Mitigações](#recomendações-e-mitigações)
9. [Lições Aprendidas](#lições-aprendidas)

---

## 1. Introdução

Breve contextualização do exercício:

* Execução de ataques de força bruta contra serviços FTP, formulário web (DVWA) e SMB no ambiente Metasploitable2, usando Medusa e ferramentas auxiliares.
* Objetivo do documento: documentar procedimentos, evidências, resultados e recomendações.

---

## 2. Objetivos

* **Objetivo principal:** validar mecanismos de autenticação e demonstrar vulnerabilidades por força bruta em ambiente controlado.
* **Objetivos secundários:**

  * Testar o Medusa em serviços FTP/SMB.
  * Automatizar tentativas em formulário web (DVWA).
  * Avaliar eficácia de wordlists simples.
  * Propor mitigação.

---

## 3. Escopo e Restrições

* **Escopo:** VMs `Kali Linux (127.0.0.1)` e `Metasploitable2 (192.168.56.101)` — host-only.
* **Serviços alvo:** FTP (vsftpd), formulário DVWA, SMB.
* **Restrições:** testes executados apenas em laboratório; nenhuma infraestrutura externa foi afetada.

---

## 4. Arquitetura do Ambiente de Teste

* **Topologia:**
  * Kali Linux — Host-only network `vboxnet0` 
  * Metasploitable2 — Host-only network 
* **Recursos/versões:** Kali Rolling, Metasploitable2 — versão padrão.

Todas as evidencias estão no arquivo **Ataque de Força Bruta _Medusa_Metasploitable2.pdf**

---

## 5. Metodologia

* Enumeração prévia (nmap e smbclient).
* Ataque de força bruta com Medusa contra FTP e SMB (password spraying).
* Automação de brute force em formulário DVWA com medusa.
* Coleta de evidências (prints de tela, logs, outputs do Medusa, tcpdump se aplicável, todas disponiveis no documento **Ataque de Força Bruta _Medusa_Metasploitable2.pdf**).

---

## 6. Ferramentas e Wordlists

* **Ferramentas usadas:**

  * `medusa`, `nmap`, `smbclient`.

* **Wordlists utilizadas:**
  
  * `users.txt`
  * `pass.txt`
  * `smb_users.txt` (lista de usuários para password spraying)
  * `senhas_spray.txt` (lista de senhas para password spraying)


---

## 7. Execução dos Testes (passo a passo)

> disponivel no documento **Ataque de Força Bruta _Medusa_Metasploitable2.pdf**

---

## 8. Recomendações e Mitigações

### Autenticação e senhas

* Política de senhas fortes (complexidade e tamanho mínimo).
* Bloqueio de conta após N tentativas (rate-limiting / lockout).
* Implementar autenticação multifator (MFA).
* Evitar contas com senhas padrão/sem alteração.

### Serviços expostos

* Desabilitar serviços não necessários (ex.: FTP) ou restringir por firewall.
* Preferir SFTP/FTPS em vez de FTP simples.
* Atualizar e hardenar serviços.

### Monitoramento e Detecção

* Habilitar logs detalhados e alertas para falhas de login em massa.
* Integrar IDS/IPS e soluções de correlação (SIEM).
* Implementar bloqueio por IP temporário (Ex.: fail2ban).

### Segurança Web (formularios)

* Proteção contra brute force (CAPTCHA, rate-limit).
* Tratar sessões e cookies corretamente (Secure, HttpOnly).
* Implementar WAF e validar/sanitizar input.

---

## 9. Lições Aprendidas 

* O que funcionou bem: facilidade de uso do Medusa para demonstração.
* O que melhorar: usar wordlists mais realistas (SecLists), testar contramedidas (fail2ban), automatizar coleta de logs.

---
