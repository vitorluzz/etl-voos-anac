# ✈️ Data Engineering Project - Ocorrências de Voos **ANAC**

## 📌 Descrição

Este projeto tem como objetivo construir uma pipeline de engenharia de dados para coletar, transformar, armazenar e analisar dados de **ocorrências aeronáuticas** disponibilizadas pela **ANAC** e **CENIPA**, promovendo insights relevantes sobre a segurança operacional da aviação civil brasileira.

O projeto segue as boas práticas de arquitetura moderna de dados, priorizando modularidade, rastreabilidade, versionamento, validação e automação.


# 📑 Glossário de Campos e Siglas

| Nome da Coluna | Sigla |
|-------------------------------|--------|
| Número da Ocorrência | NR_OCR |
| Número da Ficha | NR_FI |
| Operador Padronizado | OP_PDR |
| Classificação da Ocorrência | CLAS_OCR |
| Data da Ocorrência | DT_OCR |
| Hora da Ocorrência | H_OCR |
| Município | MCP |
| Unidade Federativa (UF) | UF |
| Região | RG |
| Descrição do Tipo | DCRI_TP |
| Código ICAO | ICAO |
| Latitude | LATD |
| Longitude | LONG |
| Tipo de Aeródromo | TP_ADRM |
| Histórico | HIST |
| Matrícula | MTCL |
| Categoria da Aeronave | CATG_ANV |
| Operador | OPOR |
| Tipo de Ocorrência | TP_OCR |
| Fase da Operação | FA_OP |
| Operação | OPCAO |
| Danos à Aeronave | DAN_ANV |
| Aeródromo de Destino | ADRM_DSTN |
| Aeródromo de Origem | ADRM_ORGM |
| Lesões Fatais Tripulantes | LS_FTL_TRPL |
| Lesões Fatais Terceiros | LS_FTL_TCOS |
| Lesoes Fatais Passageiros | LS_FTL_PSGO |
| Lesões Graves Tripulantes | LS_GV_TRPL |
| Lesões Graves Passageiros | LS_GV_PSGO |
| Lesões Graves Terceiros | LS_GV_TCOS |
| Lesões Leves Tripulantes | LS_LV_TRPL |
| Lesões Leves Passageiros | LS_LV_PSGO |
| Lesões Leves Terceiros | LS_LV_TCOS |
| Ilesos Tripulantes | IL_TRPL |
| Ilesos Passageiros | IL_PSGO |
| Lesões Desconhecidas Tripulantes | LS_DESC_TRPL |
| Lesões Desconhecidas Passageiros | LS_DESC_PSGO |
| Lesões Desconhecidas Terceiros | LS_DESC_TCOS |
| Modelo | MDL |
| CLS | CLS |
| Tipo ICAO | TP_ICAO |
| PMD | PMD |
| Número de Assentos | NR_ASTS |
| Nome do Fabricante | NM_FBRC |
| PSSO | PSSO |

> 📘 As abreviações deste glossário foram baseadas no **Manual MD33-M-02** do Ministério da Defesa:  
> [Manual de Abreviaturas, Siglas, Símbolos e Convenções Cartográficas (MD33)](https://www.gov.br/defesa/pt-br/arquivos/File/legislacao/emcfa/publicacoes/manual-md33-m-02-manual-de-abreviaturas-siglas-simbolos-e-convencoes-cartograficas.pdf/view)

---

## 🔠 Siglas e Abreviações

| Sigla     | Significado |
|-----------|-------------|
| **ANAC**  | Agência Nacional de Aviação Civil |
| **CA**    | Certificado de Aeronavegabilidade |
| **CAVOK** | Visibilidade ≥ 10 km, nenhuma nuvem abaixo de 1.500 metros ou do setor mais alto, ausência de CB e fenômenos meteorológicos significativos |
| **CB**    | Cumulonimbus (tipo de nuvem associada a turbulência severa) |
| **CENIPA**| Centro de Investigação e Prevenção de Acidentes Aeronáuticos |
| **CG**    | Centro de Gravidade |
| **CM**    | Certificado de Matrícula |
| **CMA**   | Certificado Médico Aeronáutico |
| **DCTA**  | Departamento de Ciência e Tecnologia Aeroespacial |
| **DINACIA** | Dirección Nacional de Aviación Civil e Infraestructura Aeronáutica |
| **FAER**  | Fora de Aeródromo |
| **FL**    | Flight Level (nível de voo) |
| **IAE**   | Instituto de Aeronáutica e Espaço |
| **IFR**   | Instrument Flight Rules (Regras de Voo por Instrumentos) |
| **INFRAERO** | Empresa Brasileira de Infraestrutura Aeroportuária |
| **Lat**   | Latitude |
| **Long**  | Longitude |
| **METAR** | Meteorological Aerodrome Report (Boletim Meteorológico de Aeródromo) |
| **MLTE**  | Habilitação de classe de aviões multimotores terrestres |
| **MNTE**  | Habilitação de classe de aviões monomotores terrestres |
| **PLA**   | Licença de Piloto de Linha Aérea - Avião |
| **RF**    | Relatório Final |
| **RS**    | Recomendação de Segurança |
| **SBFL**  | Código ICAO do Aeroporto Internacional de Florianópolis |
| **SC**    | Estado de Santa Catarina |
| **SERIPA**| Serviço Regional de Investigação e Prevenção de Acidentes Aeronáuticos |
| **SIPAER**| Sistema de Investigação e Prevenção de Acidentes Aeronáuticos |
| **SUAA**  | Código ICAO do Aeroporto Internacional Ángel S. Adami (Montevidéu) |
| **TWR-FL**| Torre de Controle de Florianópolis |
| **UTC**   | Universal Time Coordinated (Tempo Universal Coordenado) |
| **VFR**   | Visual Flight Rules (Regras de Voo Visual) |

---


## 🗂️ Fontes Oficiais

- **Relatórios Finais – CENIPA**  
  [https://sistema.cenipa.fab.mil.br/cenipa/paginas/relatorios/relatorios.php](https://sistema.cenipa.fab.mil.br/cenipa/paginas/relatorios/relatorios.php)

- **Lista de Ocorrências Aeronáuticas – SIPAER**  
  [https://painelsipaer.cenipa.fab.mil.br/extensions/Sipaer/Ocorrencias.html](https://painelsipaer.cenipa.fab.mil.br/extensions/Sipaer/Ocorrencias.html)

- **Recomendações de Segurança – CENIPA**  
  [https://sistema.cenipa.fab.mil.br/cenipa/paginas/relatorios/recomendacoes.php](https://sistema.cenipa.fab.mil.br/cenipa/paginas/relatorios/recomendacoes.php)

---

📌 _Última atualização: 01 de julho de 2025_  
👤 _Responsável técnico: João Vitor Luz – Engenheiro de Dados_