# Slide Outline — Seminário Cacti & SNMP (UFMA • REDES 2026-2)

## Metadados Institucionais e Equipe:
- **Instituição:** UNIVERSIDADE FEDERAL DO MARANHÃO (UFMA)
- **Logotipo Oficial:** Transparente (PNG nativo, sem caixa de fundo, filtro branco de alto contraste para tema dark)
- **Disciplina:** Comunicação de Dados e Redes de Computadores (Semestre 2026-2)
- **Assunto Oficial para Envio:** `Seminário sobre PROTO/SOFT – REDES 2026-2`
- **Tema:** Monitoramento e Gerência de Redes com Cacti & SNMP
- **Duração Total:** 25 minutos

---

### Integrantes da Equipe:
- **Ronaldy Lima França**
- **Luã Coimbra Santiago Saunders**
- **Felipe Augusto Sousa De Almada**

---

### Estrutura das Partes do Seminário (25 min — 23 Slides):
1. **Parte 1 (~7 min — Slides 01 a 11):**
   - **Slide 01:** Capa Editorial com UFMA e Integrantes na vertical.
   - **Slide 02:** Roteiro & Pipeline Geral dos 3 Blocos.
   - **Slide 03 (Contexto):** O Problema Real: Gerenciando Redes "Às Cegas" (Gestão Reativa vs. Proativa).
   - **Slide 04 (Definição):** O Que é o Cacti & A Solução de Telemetria (Tripé: SNMP, RRDtool e Web LAMP).
   - **Slide 05:** Enquadramento Teórico no Modelo ISO FCAPS (Protagonismo em Performance e apoio a Faults).
   - **Slide 06:** Arquitetura LAMP & Segregação de Dados (Acrônimo vertical L-A-M-P, origem histórica de 2001 e resiliência da stack, MySQL para metadados e RRDtool para tráfego).
   - **Slide 07:** O Mecanismo RRDtool: O Buffer Circular (Funcionamento em 3 passos: arquivo fixo de ~150 KB, avanço/sobrescrita a cada 5 min e detecção de quedas com NaN).
   - **Slide 08:** Pipeline de Consolidação: RRAs (Step 5min -> 30min -> 2h -> 1dia).
   - **Slide 09:** Motores de Coleta: O Desafio da Escala (Conceito de Nó e OID, fila sequencial do cmd.php vs. varredura paralela multithread do Spine em C).
   - **Slide 10:** Automação com Templates & Árvores (Propósito: eliminar trabalho manual com moldes de dados, gráficos e dispositivos, e organização em pastas por Campus).
   - **Slide 11:** Análise Crítica: Trade-offs de Engenharia (Cards de vantagens e limitações justificadas: GPLv2 custo zero, RRDtool previsível e multi-fabricante vs. sem alertas nativos, latência de 5 min e curadoria XML).

2. **Parte 2 (~9 min — Slides 12 a 16):**
   - **Slide 12:** Transição Parte 2.
   - **Slide 13:** Fluxo de Telas no Cacti & Plugins NOC (Network Weathermap e Thold).
   - **Slide 14:** SNMP sobre UDP (Porta 161 para consultas síncronas e Porta 162 para Traps assíncronas).
   - **Slide 15:** Estrutura da MIB-II & Árvore Hierárquica de OIDs (`ifInOctets` e `ifOutOctets`).
   - **Slide 16:** Dissecação em bytes da PDU SNMPv2c (Version, Community, Type, Request-ID, Error, VarBinds).

3. **Parte 3 (~9 min — Slides 17 a 23):**
   - **Slide 17:** Transição Parte 3.
   - **Slide 18:** Topologia de Bancada no Cisco Packet Tracer (Roteador 1941, Catalyst 2960 e Servidor Cacti).
   - **Slide 19:** Configuração do Agente no Cisco IOS CLI (Comunidade RO e restrição mandatória por ACL 10).
   - **Slide 20:** A Matemática da Banda (Cálculo de delta em bps) e Mitigação de Overflow de 32 bits com RFC 2863 (64 bits).
   - **Slide 21:** Renderização Gráfica do Cacti (Área verde Inbound e linha azul Outbound).
   - **Slide 22:** Conclusão & Coexistência Tecnológica (Cacti/RRDtool + Prometheus/Grafana).
   - **Slide 23:** Referências Bibliográficas Completas (Norma ABNT NBR 6023:2018).
