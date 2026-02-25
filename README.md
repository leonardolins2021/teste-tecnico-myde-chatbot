Chatbot AtlasX Logística - Arquitetura Modular Blip – LEONARDO LINS

Este projeto foi desenvolvido como parte do teste técnico para a vaga de Desenvolvedor de Chatbot na Myde. O sistema utiliza a plataforma Blip e segue uma arquitetura modularizada para garantir escalabilidade, performance e facilidade de manutenção.
Estrutura do Projeto
O ecossistema é composto por 8 chatbots independentes integrados via Roteador:
1.   Roteador Principal: Gerencia o fluxo de entrada e o contexto entre bots.
2.   Boas-vindas: Recepção inicial e identificação do propósito do contato.
3.   Validação CPF/CNPJ: Módulo de segurança que verifica o formato do documento e consulta a base de dados via API.
4.   Chatbot IA (Cadastro): Utiliza inteligência para coleta dinâmica de dados de clientes não encontrados.
5.   Chatbot Principal: Menu de serviços para clientes já autenticados.
6.   Atendimento Humano: Transbordo para suporte manual em casos críticos.
7.   Cascata de Validação: Tratamento de falhas de integração e regras de fallback.
8.   Finalização: Encerramento padronizado da sessão.
   
Tecnologias e Integrações

Plataforma: Blip (Builder e Roteador).
Autenticação: Integração com Amazon Cognito (OAuth2) via método POST para geração de tokens Bearer dinâmicos.
API de Dados: Consumo de endpoints AWS Lambda para consulta e gravação de registros (status 200 para sucesso e 404 para novo cadastro).
Scripts: Processamento de dados via Node.js para tratamento de variáveis e objetos JSON.Decisões Arquiteturais
Modularização: Separação por responsabilidades para reduzir erros e permitir o reaproveitamento de componentes.
Tratamento de Erros: Implementação de regras de fallback para status HTTP 500/503, garantindo que o usuário nunca fique sem resposta.
Contexto Global: Uso do contexto do roteador para que o CPF/CNPJ digitado no bot de validação seja automaticamente aproveitado pelo bot de cadastro (IA).

Cenários de Teste Implementados

Sucesso: Cliente encontrado $\rightarrow$ Direcionado ao Menu Principal.
Cadastro: Cliente inexistente $\rightarrow$ Coleta inteligente via IA $\rightarrow$ Registro via POST API.
Fallback: Erro de integração com servidor Amazon $ \rightarrow$ Direcionamento para Cascata de Validação.
