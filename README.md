# 🛠️ Laboratório 01: Diagnóstico de Rede Local e Testes de Conectividade N1

**Técnico Responsável:** Gustavo Santos  
**Data de Execução:** 07/09/2026  
**Ambiente:** Estação Windows — Adaptador Ethernet / Wi-Fi

---

## 📌 Visão Geral do Projeto
Documentação prática de análise da interface de rede, validação de conectividade em camadas (Local -> Gateway -> WAN -> DNS) e roteiro operacional de suporte técnico para chamados de nível N1 (Helpdesk).

---

## 📐 1. Mapeamento da Interface de Rede

Dados extraídos via `ipconfig /all` no Prompt de Comando:

| Parâmetro | Valor Identificado | Descrição Técnica |
| :--- | :--- | :--- |
| **Endereço IPv4** | `192.168.1.150` | Endereço privado atribuído à máquina |
| **Máscara de Sub-rede** | `255.255.255.0` | Rede de Classe C (/24) |
| **Gateway Padrão** | `192.168.1.1` | IP do roteador local de saída |
| **Servidores DNS** | `8.8.8.8` / `1.1.1.1` | Google DNS / Cloudflare DNS |

---

## 🧪 2. Matriz de Testes de Conectividade

1. **Loopback (`ping 127.0.0.1`):** Resposta de `<1ms` (0% perda). Validação da pilha TCP/IP e driver de rede local.
2. **Gateway Padrão (`ping 192.168.1.1`):** Resposta média de `2ms` (0% perda). Comunicação física e lógica com o roteador ativa.
3. **Saída Externa (`ping 8.8.8.8`):** Resposta de `15ms` (0% perda). Conexão com a internet operando normalmente.
4. **Resolução de Nomes (`nslookup google.com`):** Retornou IP válido do domínio sem timeout. Servidor DNS funcional.

---

## 📷 3. Evidência de Execução (Terminal)

![Captura do Terminal de Comando](./img/terminal-ipconfig.jfif)

---

## 🔍 4. Roteiro Operacional de Troubleshooting (N1)

> **Cenário:** O usuário relata que o ERP/Sistema de Vendas perdeu a conexão com o servidor.

* **Etapa 1:** Executar `ipconfig` para validar se a máquina possui IP válido na sub-rede (`192.168.1.x`) ou se caiu na faixa de APIPA (`169.254.x.x`).
* **Etapa 2:** Disparar `ping 192.168.1.1` para testar o meio físico (cabo/Wi-Fi/switch). Se houver perda, isolar a placa de rede ou ponto de acesso.
* **Etapa 3:** Disparar `ping 8.8.8.8` e `nslookup google.com` para diferenciar falhas de link WAN de problemas exclusivos de resolução de nomes (DNS).