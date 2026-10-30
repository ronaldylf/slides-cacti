# Laboratório executado no Cisco Packet Tracer 9.0.1

Data: 30/10/2026. Ambiente simulado, executado no Windows.

## Rede salva

Abrir Laboratorio_SNMP_UFMA.pkt no Packet Tracer.

- PC0 (gerência): 192.168.1.100/24, gateway 192.168.1.1.
- PC1 (tráfego): 192.168.1.101/24, gateway 192.168.1.1.
- Router0, hostname R1-REDES: Gi0/0 em 192.168.1.1/24.
- Switch0: Catalyst 2960.
- Os três enlaces ficaram ativos. O cabeamento automático usou portas disponíveis do switch.

## Resultados observados

1. Configuração de SNMP com `snmp-server community REDES2026 RO` aceita.
2. No PC0, Desktop > MIB Browser > Advanced: destino 192.168.1.1, porta 161, Read Community REDES2026, versão v2.
3. Operação GET, OID .1.3.6.1.2.1.1.5.0: resposta R1-REDES, tipo OctetString.
4. Consulta de descrição de interfaces: o navegador retornou Vlan1, GigabitEthernet0/0 e GigabitEthernet0/1. O simulador exibiu a tabela com índices próprios.
5. Consulta de estado .1.3.6.1.2.1.2.2.1.8.2: o navegador exibiu down, up e down na ordem das interfaces. A Gi0/0 conectada aparece up.
6. No PC1, Desktop > Command Prompt: `ping 192.168.1.1` retornou quatro respostas em quatro envios, com 0% de perdas.

## Limitações observadas

- O Cisco 1941 simulado rejeitou `snmp-server community REDES2026 RO 10`, além de `snmp-server location` e `snmp-server contact`. A configuração final usa a comunidade RO sem associação à ACL. A ACL criada inicialmente foi removida.
- As consultas .1.3.6.1.2.1.2.2.1.10 e .1.3.6.1.2.1.2.2.1.10.2 retornaram “No such name”. Não foi obtida taxa de tráfego via ifInOctets nesta execução. Isso documenta os testes realizados, sem afirmar que todas as combinações possíveis do simulador foram esgotadas.
- O teste do Packet Tracer permanece separado da coleta real do Windows descrita abaixo.

## Repetir a demonstração

1. Abrir o projeto .pkt.
2. Abrir PC0 > Desktop > MIB Browser e informar os parâmetros acima, caso não estejam preenchidos.
3. Consultar sysName para mostrar a resposta R1-REDES.
4. Consultar o estado das interfaces e relacionar o valor up ao enlace ativo.
5. Abrir PC1 > Desktop > Command Prompt e repetir o ping.
6. Explicar que uma instalação real do Cacti faz consultas periódicas a agentes alcançáveis e usa contadores compatíveis para os gráficos.

## Capturas

- prints/01_ip_pc_gerencia.png: IP, máscara e gateway.
- prints/02_parametros_snmp.png: destino, porta e versão da consulta.
- prints/03_get_sysname.png: consulta e resposta confirmada.
- prints/04_limite_contador.png: mensagem de erro do contador.
- prints/05_estado_interfaces.png: estados retornados.
- prints/06_ping_pc1.png: teste com quatro respostas, sem perdas.
- prints/07_topologia.png: rede executada com enlaces ativos.

Nos slides 20 a 24, pressione N para ver o roteiro de fala atualizado. Os demais slides mantêm o conteúdo do repositório fornecido. As capturas principais estão incorporadas no HTML.


## Etapa real: Cacti no Windows

O Cacti foi instalado e atualizado para 1.2.31. O login foi realizado e o assistente de instalação foi concluído com autorização para aceitar a licença GPL.

- URL local: http://localhost/cacti/
- Dispositivo: LAB Windows - Coleta SNMP real.
- Agente: Net-SNMP 5.9.3, atendendo somente em 127.0.0.1:1161.
- SNMPv2c, comunidade de leitura REDES2026.
- Interface real: Realtek PCIe GbE Family Controller, ifIndex 12.
- OIDs: entrada .1.3.6.1.2.1.2.2.1.10.12 e saída .1.3.6.1.2.1.2.2.1.16.12.
- Perfil Cacti: coleta de 1 minuto. Gráfico local de ID 8.
- Janela exportada: 30/10/2026, 15h34 a 15h40, horário de Brasília.
- O gráfico é o original produzido pelo Cacti/RRDtool. Foram preservados SVG, captura recortada e captura com o contexto do painel.
- As consultas adicionais em coleta_snmp_windows.csv usam aproximadamente 30 segundos. Os números do slide 20 vêm das duas últimas linhas desse arquivo.

Para repetir a demonstração, abra Graphs > Preview no Cacti e filtre por Trafego real. As capturas e o HTML funcionam sem depender da execução ao vivo.

### Observações para reabrir o laboratório

O servidor web e o banco foram instalados como serviços do Windows. O agente SNMP e a coleta de um minuto foram iniciados como processos locais de laboratório. O agente precisa estar em execução para novas leituras em 127.0.0.1:1161. O instalador também criou uma tarefa periódica do Cacti, mas o processo usado nesta demonstração ajustou a execução para o intervalo de um minuto, com duração limitada.

Foi necessário normalizar o separador dos caminhos de execução no auxiliar exec_background do Cacti para executar o coletor no Windows. Os controles de escape de comandos foram mantidos. O fuso do Cacti foi ajustado para America/Sao_Paulo. As cópias de segurança da instalação anterior foram preservadas localmente.

O administrador local usa a senha gerada pelo instalador, no arquivo Cacti-Passwords.txt junto ao instalador. Esse arquivo não faz parte do pacote de entrega e a senha não está nos slides.

### Novos arquivos de evidência

- prints/08_cacti_dispositivo.jpg: dispositivo monitorado em estado Up.
- prints/09_cacti_grafico_real.jpg: visualizador do Cacti com o gráfico real.
- grafico_cacti_real.svg: gráfico original exportado, com rótulos e legenda.
- grafico_cacti_real.jpg: recorte do gráfico no navegador.
- coleta_snmp_windows.csv: leituras adicionais do agente, com instantes UTC e taxas calculadas.

A apresentação FINAL substitui a primeira versão de preparação e a versão intermediária com testes.
