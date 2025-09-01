# ✈️ Data Engineering Project – Ocorrências de Voos **ANAC/CENIPA**

## 🎯 Contexto e Motivação do Projeto

Este projeto tem como objetivo desenvolver uma **pipeline de engenharia de dados robusta e confiável**, voltada à **coleta, transformação, armazenamento e análise** dos dados de **ocorrências aeronáuticas** disponibilizados pelo **CENIPA** e pela **ANAC** — fontes oficiais e fundamentais para o monitoramento de incidentes e acidentes que envolvem vidas humanas na **aviação civil brasileira**.


Este projeto surge a partir de uma constatação alarmante: **mesmo sendo o CENIPA um órgão central na investigação e registro de ocorrências aeronáuticas no Brasil — lidando diretamente com eventos que envolvem riscos à vida humana — os dados disponibilizados por essa instituição carecem de cuidados básicos de qualidade e integridade**.

Durante a análise das bases de dados, foi observado:

- **Campos críticos deixados em branco**;
- **Inúmeros erros de digitação**;
- **Ausência de padronização**;
- **Informações contraditórias dentro de um mesmo registro**.

São falhas que **não deveriam existir** em um sistema responsável por registrar **acidentes e incidentes aéreos**, muitos dos quais com **vítimas fatais**.

Essa **falta de zelo com os dados** compromete diretamente:

- A **transparência**;
- A **rastreabilidade das informações**;
- E a **formulação de políticas públicas eficazes** para a segurança da aviação civil!

Em outras palavras: **estamos diante de uma base de dados que, embora venha de uma fonte oficial e sensível, não está sendo tratada com o rigor técnico que sua relevância exige**.

---

Nosso projeto, portanto, **não apenas implementa uma pipeline de engenharia de dados moderna**, mas também **atua como uma iniciativa corretiva**, promovendo:

- **Validação**;
- **Saneamento**;
- **Padronização**;
- E **enriquecimento das informações**.

O objetivo é **extrair valor confiável de uma base que, infelizmente, reflete descuido em sua gestão**.

---

## 🧠 Abordagem Técnica

O projeto adota princípios da **arquitetura moderna de dados**, com foco em:

- 🧩 **Modularidade**  
- 🔎 **Rastreabilidade**  
- 🕒 **Versionamento de dados e transformações**  
- ✅ **Validação automatizada**  
- 📊 **Governança e qualidade da informação**

---



# 📑 Dicionário de Dados (Data Dictionary)

> Um dicionário de dados é essencial para garantir a clareza, a consistência e a integridade no uso de informações em um projeto. Ele documenta de forma padronizada o significado, o tipo, o formato e os valores esperados de cada coluna de um conjunto de dados, permitindo que diferentes profissionais — como engenheiros, analistas e cientistas de dados — compreendam e utilizem os dados corretamente. Além disso, facilita a manutenção de pipelines, promove a governança e reduz erros de interpretação ao longo de todo o ciclo de vida dos dados.

| Nome da Coluna                       | Sigla         | Tipo           | Formato         | Descrição                                                 | Domínio / Valores Possíveis                                                |
|-------------------------------------|---------------|----------------|------------------|-----------------------------------------------------------|-----------------------------------------------------------------------------|
| Número da Ocorrência                | NR_OCR        | int64          | Número inteiro   | Identificador único da ocorrência                         | —                                                                           |
| Número da Ficha                     | NR_FI         | object         | Texto            | Código da ficha associada à ocorrência                    | —                                                                           |
| Operador Padronizado               | OP_PDR        | object         | Texto            | Nome padronizado do operador da aeronave                  | —                                                                           |
| Classificação da Ocorrência         | CLAS_OCR      | object         | Texto            | Classificação da ocorrência                               | Incidente, Ocorrência Anormal, Acidente, Ocorrência de Solo, etc.          |
| Data da Ocorrência                  | DT_OCR        | datetime64[ns] | AAAA-MM-DD       | Data do evento                                            | —                                                                           |
| Hora da Ocorrência                  | H_OCR         | object         | HH:MM            | Horário aproximado da ocorrência                          | —                                                                           |
| Município                           | MCP           | object         | Texto            | Nome do município da ocorrência                           | —                                                                           |
| Unidade Federativa (UF)            | UF            | object         | Texto            | Estado da federação (sigla)                               | SP, RJ, MG, ...                                                             |
| Região Geográfica (RG)             | RG            | object         | Texto            | Região do país                                            | Norte, Centro-Oeste, Sudeste, Sul, Nordeste                                |
| Descrição do Tipo                   | DCRI_TP       | object         | Texto            | Tipo da decorrência registrada                            | Colisão no Solo, Fogo, Falha de Sistema, Outros...                         |
| Código ICAO                         | ICAO          | object         | Texto (4 letras) | Código ICAO do aeródromo envolvido                        | Ex: SBSP, SBRJ                                                              |
| Latitude                            | LATD          | float64        | Grau decimal     | Latitude geográfica do evento                             | —                                                                           |
| Longitude                           | LONG          | float64        | Grau decimal     | Longitude geográfica do evento                            | —                                                                           |
| Tipo de Aeródromo                   | TP_ADRM       | object         | Texto            | Tipo do aeródromo                                         | Público, Privado, Militar, FAER, Não identificado                          |
| Histórico                           | HIST          | object         | Texto            | Descrição textual da ocorrência                           | —                                                                           |
| Matrícula                           | MTCL          | object         | Texto            | Registro da aeronave                                      | PR-ABC, PTCZC, CSTOF, etc.                                                  |
| Categoria da Aeronave              | CATG_ANV      | object         | Texto            | Categoria da aeronave envolvida                          | Militar, Estrangeira, Sem matrícula, TRP, ADF, etc.                         |
| Operador                            | OPOR          | object         | Texto            | Nome do operador da aeronave                              | —                                                                           |
| Tipo de Ocorrência                 | TP_OCR        | object         | Texto            | Causa principal da ocorrência                             | OTHR, GCOL, F-NI, SCF-PP, BIRD, etc.                                        |
| Fase da Operação                   | FA_OP         | object         | Texto            | Fase do voo em que ocorreu                                | Pouso, Subida, Táxi, Cruzeiro, Arremetida, Indeterminada...                |
| Operação                            | OPCAO         | object         | Texto            | Tipo de operação da aeronave                              | Voo Privado, Voo Regular, Operação Pública, Táxi Aéreo, etc.               |
| Danos à Aeronave                   | DAN_ANV       | object         | Texto            | Grau de dano na aeronave                                  | Nenhum, Leve, Substancial, Destruída, Desconhecida                         |
| Aeródromo de Destino               | ADRM_DSTN     | object         | Texto            | Código ou nome do destino previsto                        | —                                                                           |
| Aeródromo de Origem                | ADRM_ORGM     | object         | Texto            | Código ou nome da origem do voo                           | —                                                                           |
| Lesões Fatais Tripulantes          | LS_FTL_TRPL   | int64          | Número inteiro   | Número de tripulantes mortos                              | —                                                                           |
| Lesões Fatais Terceiros            | LS_FTL_TCOS   | int64          | Número inteiro   | Número de terceiros mortos                                | —                                                                           |
| Lesões Fatais Passageiros          | LS_FTL_PSGO   | int64          | Número inteiro   | Número de passageiros mortos                              | —                                                                           |
| Lesões Graves Tripulantes          | LS_GV_TRPL    | int64          | Número inteiro   | Número de tripulantes gravemente feridos                 | —                                                                           |
| Lesões Graves Passageiros          | LS_GV_PSGO    | int64          | Número inteiro   | Número de passageiros gravemente feridos                 | —                                                                           |
| Lesões Graves Terceiros            | LS_GV_TCOS    | int64          | Número inteiro   | Número de terceiros gravemente feridos                   | —                                                                           |
| Lesões Leves Tripulantes           | LS_LV_TRPL    | int64          | Número inteiro   | Número de tripulantes levemente feridos                  | —                                                                           |
| Lesões Leves Passageiros           | LS_LV_PSGO    | int64          | Número inteiro   | Número de passageiros levemente feridos                  | —                                                                           |
| Lesões Leves Terceiros             | LS_LV_TCOS    | int64          | Número inteiro   | Número de terceiros levemente feridos                    | —                                                                           |
| Ilesos Tripulantes                 | IL_TRPL       | int64          | Número inteiro   | Número de tripulantes ilesos                              | —                                                                           |
| Ilesos Passageiros                 | IL_PSGO       | int64          | Número inteiro   | Número de passageiros ilesos                              | —                                                                           |
| Lesões Desconhecidas Tripulantes  | LS_DESC_TRPL  | int64          | Número inteiro   | Tripulantes com condição desconhecida                    | —                                                                           |
| Lesões Desconhecidas Passageiros  | LS_DESC_PSGO  | int64          | Número inteiro   | Passageiros com condição desconhecida                    | —                                                                           |
| Lesões Desconhecidas Terceiros    | LS_DESC_TCOS  | int64          | Número inteiro   | Terceiros com condição desconhecida                      | —                                                                           |
| Modelo                             | MDL           | object         | Texto            | Modelo da aeronave                                        | —                                                                           |
| Classe                             | CLS           | object         | Texto            | Classe da aeronave (porte, tipo de operação, etc.)       | —                                                                           |
| Tipo ICAO                          | TP_ICAO       | object         | Texto            | Código do tipo ICAO da aeronave                          | —                                                                           |
| Peso Máximo de Decolagem           | PMD           | float64        | Número decimal   | Peso máximo de decolagem da aeronave (em kg)             | —                                                                           |
| Número de Assentos                 | NR_ASTS       | int64          | Número inteiro   | Número total de assentos da aeronave                     | —                                                                           |
| Nome do Fabricante                 | NM_FBRC       | object         | Texto            | Nome do fabricante da aeronave                           | —                                                                           |
| Possuía Pouso Autorizado           | PSSO          | bool           | True/False       | Indica se havia autorização de pouso                     | True, False                                                                |


> 📘 As abreviações deste glossário foram baseadas no **Manual MD33-M-02** do Ministério da Defesa:  
> [Manual de Abreviaturas, Siglas, Símbolos e Convenções Cartográficas (MD33)](https://www.gov.br/defesa/pt-br/arquivos/File/legislacao/emcfa/publicacoes/manual-md33-m-02-manual-de-abreviaturas-siglas-simbolos-e-convencoes-cartograficas.pdf/view)

---

## 🔠 Glossário de Tipos de Ocorrências

| Sigla     | Significado (EN)                                     | Tradução (PT)                                       | Explicação |
|-----------|------------------------------------------------------|-----------------------------------------------------|------------|
| **GCOL**  | Ground Collision                                     | Colisão no Solo                                     | Envolve colisões ocorridas em solo, geralmente durante taxiamento, estacionamento ou movimentações da aeronave sem intenção de voo. |
| **F-NI**  | Fire/Smoke (Non-Impact)                              | Fogo/Fumaça (Não Causado por Impacto)               | Eventos com indícios de fogo ou fumaça sem origem clara ou com impacto limitado. A aeronave permanece sob controle. |
| **ARC**   | Abnormal Runway Contact                              | Contato Anormal com a Pista                         | Contato inadequado ou inesperado com a pista, sem necessariamente resultar em acidente grave. |
| **SCF-NP**| System/Component Failure or Malfunction – Non-Powerplant | Falha de Sistema/Componente – Não Relacionado ao Motor | Falhas técnicas em sistemas não ligados à motopropulsão (ex: trem de pouso, freios, sistemas elétricos). |
| **SCF-PP**| System/Component Failure or Malfunction – Powerplant | Falha de Sistema/Componente – Relacionado ao Motor  | Falhas no motor ou nos sistemas de propulsão, como perda de potência ou pane mecânica. |
| **BIRD**  | Birdstrike                                           | Colisão com Ave                                     | Colisão entre a aeronave e aves, em qualquer fase do voo. |
| **FUEL**  | Fuel Related Event                                   | Ocorrência Relacionada a Combustível                | Problemas com combustível, como falta, contaminação ou pane seca. |
| **RAMP**  | Ramp Operation Event                                 | Ocorrência em Solo/Pátio                            | Ocorrências durante serviços de rampa (ex: abastecimento, pushback, colisão com equipamentos). |
| **AMAN**  | Abrupt Maneuver                                      | Manobra Abrupta                                     | Manobras bruscas, não planejadas, normalmente evasivas, durante o voo ou no solo. |
| **LOC-I** | Loss of Control – In-Flight                          | Perda de Controle em Voo                            | Perda de controle da aeronave durante o voo, muitas vezes com atitudes anormais. |
| **RE**    | Runway Excursion                                     | Excursão de Pista                                   | A aeronave sai dos limites da pista durante pouso ou decolagem. |
| **CTOL**  | Collision During Takeoff or Landing                  | Colisão Durante a Decolagem ou Pouso                | Colisões com obstáculos durante a decolagem, pouso ou aproximação. |
| **LALT**  | Low Altitude Operations                               | Operações em Baixa Altitude                         | Operações realizadas próximas ao solo, típicas em voos agrícolas ou locais. |
| **WSTRW** | Windshear or Thunderstorm                            | Cisalhamento de Vento ou Tempestade                 | Condições meteorológicas severas durante o voo (turbulência extrema, granizo, vento cortante). |
| **CFIT**  | Controlled Flight Into Terrain                       | Voo Controlado Contra o Terreno                     | Colisão com o terreno mesmo com a aeronave sob controle do piloto. |
| **LOC-G** | Loss of Control – Ground                             | Perda de Controle no Solo                           | Perda de controle da aeronave durante operações no solo (pouso, taxi, decolagem). |
| **WILD**  | Wildlife                                             | Fauna Silvestre                                     | Incursões ou colisões com animais na pista (aves, antas, emas, etc.). |
| **MAC**   | Airprox / Mid-Air Conflict                           | Aproximação Perigosa / Conflito em Voo              | Perda de separação segura entre aeronaves no ar, sem colisão. |
| **EXTL**  | External Load                                        | Carga Externa                                       | Operações com cargas externas em helicópteros, como resgates ou transporte suspenso. |
| **RI**    | Runway Incursion                                     | Incursão em Pista                                   | Entrada indevida de aeronaves ou veículos na pista sem autorização. |
| **UIMC**  | Unintended Flight into IMC                           | Voo Não Intencional em Condições de Instrumento     | Aeronaves VFR que entram inadvertidamente em condições IMC (clima fechado). |
| **LOLI**  | Loss of Lifting Conditions En-route                  | Perda de Sustentação em Rota                        | Perda de sustentação causada por fatores ambientais, mecânicos ou erro do piloto. |
| **EVAC**  | Evacuation                                           | Evacuação                                           | Evacuação dos ocupantes da aeronave, com ou sem uso de escorregadeiras. |
| **ADRM**  | Aerodrome                                            | Aeródromo                                           | Ocorrências relacionadas à infraestrutura ou operação do aeródromo. |
| **MED**   | Medical                                              | Ocorrência Médica                                   | Envolve incapacitação de tripulantes, emergências médicas ou voos aeromédicos. |
| **USOS**  | Undershoot or Overshoot                              | Subutilização ou Ultrapassagem da Pista             | Toque no solo antes do início da pista (undershoot) ou além do limite (overshoot). |
| **ATM/CNS**| Air Traffic Management / Communication, Navigation, Surveillance | Gerenciamento do Tráfego Aéreo / Comunicação, Navegação, Vigilância | Incidentes com falhas em controle de tráfego, navegação ou comunicação com o ATC. |
| **TURB**  | Turbulence                                           | Turbulência                                         | Movimentos desordenados da aeronave devido a instabilidade atmosférica. |
| **ICE**   | Ice Formation                                        | Formação de Gelo                                    | Formação de gelo em superfícies da aeronave, afetando seu desempenho. |
| **F-POST**| Fire/Smoke (Post-Impact)                             | Fogo/Fumaça Após Impacto                            | Incêndio que ocorre após colisão da aeronave com o solo ou obstáculo. |
| **SEC**   | Security-related                                     | Relacionado à Segurança Pública ou Nacional         | Envolve voos clandestinos, tráfico, interceptações militares, ou ameaças à segurança. |
| **CABIN** | Cabin Safety Event                                   | Evento de Segurança na Cabine                       | Incidentes dentro da cabine, como falhas em equipamentos de segurança ou mau uso. |
| **GTOW**  | Glider Take-Off With Tow                             | Decolagem de Planador com Reboque                   | Ocorrências durante decolagem de planadores por reboque (avião ou guincho). |
| **UNK**   | Unknown                                              | Desconhecido / Indeterminado                        | Quando não se sabe em qual fase do voo ocorreu o evento ou há falta de dados. |

---

## 🗂️ Fontes Oficiais

- **Relatórios Finais – CENIPA**  
  [https://sistema.cenipa.fab.mil.br/cenipa/paginas/relatorios/relatorios.php](https://sistema.cenipa.fab.mil.br/cenipa/paginas/relatorios/relatorios.php)

- **Lista de Ocorrências Aeronáuticas – SIPAER**  
  [https://painelsipaer.cenipa.fab.mil.br/extensions/Sipaer/Ocorrencias.html](https://painelsipaer.cenipa.fab.mil.br/extensions/Sipaer/Ocorrencias.html)

- **Recomendações de Segurança – CENIPA**  
  [https://sistema.cenipa.fab.mil.br/cenipa/paginas/relatorios/recomendacoes.php](https://sistema.cenipa.fab.mil.br/cenipa/paginas/relatorios/recomendacoes.php)

- **Consultas ao Registro Aeronáutico Brasileiro (RAB)**  
  [https://sistemas.anac.gov.br/aeronaves/cons_rab.asp#matricula](https://sistemas.anac.gov.br/aeronaves/cons_rab.asp#matricula)

---


## 🤖 Prompts Utilizados com Assistente de IA

Durante o desenvolvimento deste projeto, foram utilizados **prompts com assistentes de inteligência artificial** (como o ChatGPT) para apoiar o trabalho de análise, enriquecimento e padronização dos dados. Essa prática visou aumentar a eficiência em tarefas exploratórias e automatizar classificações complexas.

### 📋 Lista de Prompts Aplicados

#### 🔍 Encontrar notícias relacionadas à ocorrência
- **Objetivo:** Localizar automaticamente notícias disponíveis na internet com base no número da ocorrência (NR_OCR) e demais dados do caso.
- **Link:** [https://chatgpt.com/share/6871205a-9054-8012-8097-d811d444c5b3]

#### ✈️ Identificar aeronave a partir da matrícula e operador
- **Objetivo:** Buscar, com base no registro da aeronave (MTCL), dados complementares sobre o modelo, fabricante e operador.
- **Link:** [https://chatgpt.com/share/6871204c-a3bc-8012-9a34-4bbb9bf14e39]

#### 🧠 Classificar tipo de ocorrência com base no histórico textual
- **Objetivo:** Sugerir uma classificação automatizada do tipo de ocorrência (TP_OCR) a partir da descrição textual do histórico do caso (HIST).
- **Link:** [https://chatgpt.com/share/689392de-379c-8001-b312-8e9b7c5f7371]

#### 🚀 Classificar fase da operação e descrição do tipo da ocorrência
- **Objetivo:** Sugerir uma classificação automatizada da descrição do tipo de ocorrência e a fase da operação onde se ocorreu o indicente com base textual do histórico do caso (HIST).
- **Link:** [https://chatgpt.com/share/68770ffb-6370-8001-82eb-0f8992fce9af]

---

> 📎 *OBS: Os resultados obtidos via IA foram sempre validados manualmente antes de sua adoção final, assegurando conformidade técnica e fidelidade factual aos dados oficiais.*

---

📌 _Última atualização: 1 de setembro de 2025_  
👤 _Responsável técnico: João Vitor Luz – Engenheiro de Dados_
