# Troubleshooting: recuperação do Zabbix após travamento do APT

## 📌 Cenário

Durante uma atualização automática do Ubuntu Server, o ambiente do Zabbix
apresentou indisponibilidade.

O MySQL foi interrompido e o Zabbix Server ficou preso durante um processo
de restart.

## 🚨 Sintomas

- Zabbix apresentando erro de conexão com o banco de dados
- MySQL em estado inactive/dead
- Zabbix Server preso em processo de restart
- APT bloqueando o reboot do servidor
- unattended-upgrade permanecendo em execução

## 🔎 Investigação

Foram utilizados comandos como:

```bash
systemctl status mysql
systemctl status zabbix-server
systemctl list-jobs
ps aux | grep -E 'apt|dpkg|unattended'
pstree
dpkg --audit
fuser /var/lib/dpkg/lock-frontend /var/lib/dpkg/lock
