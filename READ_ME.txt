README – Modelagem de Dados: Funcionários (Horista/Assalariado)
Objetivo

Este projeto tem como objetivo apresentar duas propostas de modelagem de dados para um sistema de gestão de funcionários, considerando diferentes tipos (horistas e assalariados), o uso de ENUM, tabelas segregadas versus herança, e o uso do tipo jsonb no PostgreSQL.

Tecnologias e Banco de Dados

SGBD: PostgreSQL

Tipos avançados utilizados: ENUM, JSONB, GIN Index

Justificativa Técnica das Decisões

Durante a modelagem, foram feitas escolhas com base em:

Normalização de dados para evitar redundância e manter integridade.

Reaproveitamento de atributos comuns via herança (Proposta 1).

Performance de leitura e simplicidade em abordagens mais diretas (Proposta 2).

Flexibilidade para armazenar dados semi-estruturados usando jsonb.

Modelagens Propostas
Proposta 1: Herança (Generalização/Especialização)

Nesta abordagem, temos uma tabela funcionario com os dados comuns, e duas tabelas derivadas (func_horista e func_assalariado) com os dados específicos de cada tipo de funcionário.

Vantagens

Alta coerência semântica com princípios de orientação a objetos.

Evita colunas nulas.

Reutilização de dados comuns.

Desvantagens

Requer joins para consolidar informações.

Pouco prático quando há muitos tipos de subclasses.

Ideal para:

Sistemas com regras bem definidas.

Aplicações que usam ORMs ou DDD (Domain Driven Design).

Proposta 2: Tabelas Segregadas

Cada tipo de funcionário possui uma tabela completa (com todos os campos comuns e específicos), sem herança.

Vantagens

Consultas diretas e rápidas.

Estrutura simples para bancos relacionais básicos.

Desvantagens

Redundância estrutural.

Dificuldade em aplicar regras genéricas (ex: listar todos os funcionários).

Ideal para:

Sistemas pequenos ou com foco em performance pontual.

Quando não se espera escalabilidade de tipos.

Uso de jsonb: Reflexão Crítica

O campo jsonb foi adicionado à tabela funcionario como dados_adicionais, com a proposta de armazenar informações opcionais e não estruturadas, como:

Certificações

Idiomas

Preferências pessoais

Histórico de cargos

Quando jsonb é recomendado?
| Cenário                                 | jsonb é útil? |
| --------------------------------------- | ------------- |
| Armazenar dados variáveis e opcionais   | ✅ Sim         |
| Informações com esquema instável        | ✅ Sim         |
| Armazenar logs ou histórico de mudanças | ✅ Sim         |

Quando jsonb é um problema?
| Cenário                                | jsonb é ruim? |
| -------------------------------------- | ------------- |
| Dados que precisam de validação rígida | ❌ Sim         |
| Relatórios e análises frequentes       | ❌ Sim         |
| Integração com BI e outras ferramentas | ❌ Sim         |

Considerações Técnicas

O PostgreSQL permite indexação GIN sobre colunas jsonb, o que melhora a performance, mas os índices são mais pesados.

Não é possível aplicar chaves estrangeiras, validações por tipo ou constraints dentro do JSON.

Deve ser usado com moderação e apenas quando a estrutura relacional não for suficiente.

Conclusão

A escolha entre herança ou tabelas segregadas depende do nível de complexidade e do modelo de negócios.

O uso de jsonb é poderoso, mas requer cautela e análise criteriosa.

A modelagem orientada a herança é mais limpa e organizada para sistemas com múltiplas variações de entidades.

Estrutura do Projeto

📦 modelagem-funcionarios
├── 📄 create_tables.sql       # Script completo de criação
├── 📄 README.md               # Este documento
├── 📄 inserts_exemplo.sql     # Exemplos de inserção (opcional)
└── 📄 diagramas/              # (Opcional) DERs gerados visualmente
