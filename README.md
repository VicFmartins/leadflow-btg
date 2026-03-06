Lead Flow — Sistema Automático de Geração de Leads
Autor: Vitória
Plataforma: Google Apps Script
Execução: Automática diária às 07:00 (Brasília)
Dias: Segunda a Sexta

📋 Visão Geral
Lead Flow é um sistema automático de coleta e classificação de leads de múltiplas fontes online, desenvolvido em Google Apps Script. O sistema busca potenciais clientes em YouTube, Telegram, Reddit e bases públicas de empresas (PJ), aplica scoring inteligente, deduplica informações e entrega um relatório estruturado via email com integração ao Google Sheets.

Objetivo
Identificar automaticamente pessoas e empresas com interesse em investimentos, produtos financeiros e serviços B2B, priorizando leads de alta qualidade baseado em análise de comportamento online.

🎯 Funcionalidades Principais
1. Coleta Multicanal
📺 YouTube: Análise de comentários em vídeos com queries de investimento

📱 Telegram: Monitoramento de grupos e canais de interesse

🤖 Reddit: Busca em subreddits e posts com palavras-chave

🏢 PJ: Consulta de empresas em registros públicos (CNPJ, Google Maps, BrasilAPI)

2. Scoring Inteligente
Análise de intenção através de keywords

Extração automática de contatos (email/telefone)

Classificação em 3 níveis: Quente (≥70), Novo (45-69), Frio (<45)

Detecção de spam e conteúdo irrelevante

3. Deduplicação
Remove leads duplicados por nome

Filtra bots e perfis suspeitos

Garante base limpa de prospectos únicos

4. Integração Google Sheets
Salva todos os leads em planilha persistente

Cabeçalho congelado com formatação

Histórico completo por data

Colunas: Data, Plataforma, Tipo, Nome, CNPJ, Telefone, Email, Interesse, Status, Score

5. Relatórios por Email
Email HTML com dashboard visual

Top 15 leads por score

Links diretos para perfis (WhatsApp, YouTube, Reddit, Telegram)

Anexos em JSON e CSV

6. Execução Automática
Gatilho diário via Google Apps Script

Pula fins de semana automaticamente

Tratamento de erros com notificação via email

Modo teste para execução manual

🔧 Configuração
Pré-requisitos
Google Apps Script (script.google.com)

APIs habilitadas:

YouTube Data API v3

Google Places API

Google Sheets (para salvar leads)

Gmail (para enviar relatórios)

Passo a Passo
1. Criar Projeto no Google Apps Script
text
1. Acesse script.google.com
2. Crie novo projeto
3. Nomeie como "LeadFlow"
2. Colar o Código
javascript
// Limpe o editor padrão
// Cole todo o código do projeto
// Salve (Ctrl+S)
3. Configurar Credenciais
Edite a seção "CONFIGURAÇÃO — preencha apenas estes campos":

javascript
// YouTube
const YOUTUBE_API_KEY = "COLE_SUA_CHAVE_AQUI";

// Telegram — Obtenha em my.telegram.org → API development tools
const TELEGRAM_API_ID   = "SEU_ID_AQUI";
const TELEGRAM_API_HASH = "COLE_AQUI";

// Telegram Bot Token (obtenha via @BotFather no Telegram)
const TELEGRAM_BOT_TOKEN = "COLE_AQUI";
const TELEGRAM_CHAT_ID   = "COLE_AQUI";

// Email para receber relatórios
const SEU_EMAIL = "seu@email.com";

// Horário de execução (0-23, fuso Brasília)
const HORA_EXECUCAO = 7;
4. Configurar Grupos/Canais Telegram
Edite a lista TELEGRAM_GRUPOS:

javascript
const TELEGRAM_GRUPOS = [
  "seu_grupo_1",
  "seu_grupo_2",
  "seu_canal",
  // ...
];
5. Configurar Subreddits e Termos de Busca
Customize as listas:

javascript
const REDDIT_SUBREDDITS = ["investimentos", "financaspessoais", ...];
const REDDIT_SEARCH_TERMS = ["BTG Pactual", "como investir", ...];
6. Configurar PJ (Opcional)
javascript
const GOOGLE_PLACES_API_KEY = "COLE_CHAVE_AQUI";
const GOOGLE_MAPS_CATEGORIAS = ["empresa Recife", "startup", ...];
const CNPJ_CNAES = ["6622300", "6630400", ...]; // Códigos CNAE
7. Criar Gatilho (Automação)
javascript
1. No editor, clique em "Executar"
2. Escolha a função: configurarGatilho
3. Autorize as permissões solicitadas
4. Pronto! O script rodará automaticamente todo dia às hora configurada
🚀 Uso
Modo Automático (Padrão)
O script executa automaticamente todo dia de semana às 07:00:

Coleta leads de todas as plataformas

Aplica scoring e filtra

Envia email com relatório e anexos

Salva na planilha Google Sheets

Modo Teste (Manual)
Para testar imediatamente sem aguardar a execução agendada:

javascript
1. Editor → Google Apps Script
2. Selecione a função: testarAgora
3. Execute (botão ▶)
4. Verifique o Log (View → Logs)
📊 Estrutura dos Dados
Coluna "Score" (0-100)
+18 pontos por cada keyword de intenção encontrada

+25 pontos se contém email válido

+20 pontos se contém telefone válido

+8 pontos se contém pergunta (?)

-20 pontos se texto muito curto (<15 caracteres)

0 pontos se contém palavras-chave de spam/fraude

Status
Status	Score	Significado
🔥 Quente	≥ 70	Alta probabilidade de conversão
🟢 Novo	45-69	Interesse detectado, precisa contato
❄️ Frio	< 45	Baixa probabilidade, para follow-up
Plataformas Suportadas
YouTube: Comentários em vídeos relevantes

Telegram: Mensagens em grupos/canais

Reddit: Posts e comentários em subreddits

PJ: Empresas via CNPJ, Google Maps, BrasilAPI

🔑 APIs Utilizadas
YouTube Data API v3
Busca vídeos por keyword

Extrai comentários de vídeos

Requer: YOUTUBE_API_KEY

Limite: 10.000 unidades/dia

Telegram Bot API
Acessa mensagens de grupos/canais via bot

Requer: TELEGRAM_BOT_TOKEN, TELEGRAM_CHAT_ID

Sem limite de requisições

Reddit API (JSON Endpoint)
Acessa subreddits e posts publicamente

Sem autenticação necessária

Limite: ~60 requisições/minuto

Google Places API
Busca empresas por categoria/localização

Extrai telefone, website, endereço

Requer: GOOGLE_PLACES_API_KEY

BrasilAPI (Pública)
Consulta dados de CNPJ

Sem autenticação necessária

Limite: ~10 requisições/segundo

ReceitaWS (Pública)
Busca empresas por atividade

Sem autenticação necessária

Fallback para BrasilAPI

📧 Saída: Email e Relatórios
Email HTML
Dashboard com 4 cards de resumo (Total, Quentes, Novos, por Plataforma)

Tabela com Top 15 leads

Cores temáticas: ouro (#C9A84C), verde (#2DD4A0), cinza (#7A8090)

Links diretos para perfis (WhatsApp, YouTube, Telegram, Reddit)

Anexos
JSON (leads_YYYY-MM-DD.json)

Array com todos os leads

Todos os campos estruturados

Útil para integração com CRM

CSV (leads_YYYY-MM-DD.csv)

Separador: ponto-e-vírgula (;)

Encoding: UTF-8 com BOM

Abrir no Excel sem problemas de acentuação

🛡️ Segurança e Boas Práticas
⚠️ Nunca compartilhe
API Keys (YouTube, Google Places)

Telegram Bot Token e Chat ID

Email de recebimento

💾 Backup
Google Sheets armazena histórico permanente

JSON anexado ao email diariamente

CSV para análise histórica

⏱️ Rate Limits
YouTube: 10.000 unidades/dia (suficiente para ~50 buscas)

Reddit: 60 req/minuto (respeitado pelo código)

Google Places: 150 requisições/segundo (configurado com delays)

BrasilAPI: 10 req/segundo (com Utilities.sleep)

🐛 Troubleshooting
Problema: "Erro de autenticação na API"
Solução: Verifique se as credenciais foram preenchidas corretamente e se as APIs estão habilitadas no Google Cloud Console.

Problema: "Gatilho não executa"
Solução:

Verifique se a função configurarGatilho foi executada

Em Triggers (relógio ⏰), verifique se há um trigger ativo

Autorize as permissões novamente

Problema: "Email não recebido"
Solução:

Verifique se SEU_EMAIL está correto

Teste com a função testarAgora

Verifique pastas de spam/lixo

Problema: "Planilha não criada"
Solução: O script cria automaticamente na primeira execução. Se não funcionar, crie manualmente uma planilha chamada "LeadFlow BTG — Base de Leads".

📈 Fluxo de Execução
text
┌─ Gatilho Diário (07:00 ou testarAgora)
│
├─ 1️⃣ YouTube Scraper
│  └─ Busca queries → Extrai comentários → Score & Filter
│
├─ 2️⃣ Telegram Scraper
│  └─ Acessa grupos/canais → Filtra mensagens → Score & Filter
│
├─ 3️⃣ Reddit Scraper
│  └─ Busca subreddits → Extrai posts/comentários → Score & Filter
│
├─ 4️⃣ PJ Scraper
│  └─ BrasilAPI → ReceitaWS → Google Maps → Extrai contatos
│
├─ 5️⃣ Deduplicação
│  └─ Remove duplicatas por nome/ID
│
├─ 6️⃣ Ordenação
│  └─ Ordena por Score (decrescente)
│
├─ 7️⃣ Envio de Email
│  └─ HTML + JSON + CSV
│
└─ 8️⃣ Salvo no Sheets
   └─ Adiciona nova linha com todos os leads
🚦 Status de Execução
Monitore o progresso em Execuções (botão ⏱️):

✅ Executado: Tudo funcionou

⚠️ Avisado: Funcionou com warnings

❌ Erro: Algo deu errado (verifique logs)

📝 Logs
Para debugar:

javascript
1. Editor → View → Logs
2. Veja mensagens de progresso com emojis
3. Identifique em qual etapa falhou
4. Verifique credenciais e limites de API
🔄 Próximas Melhorias (Ideias)
 Integração com CRM (Pipedrive, HubSpot)

 Análise de sentimento (NLP)

 Segmentação automática por nicho

 Dashboard interativo no Google Sheets com gráficos

 Notificações via Telegram para leads "Quentes"

 A/B testing de mensagens de prospecção

 Histórico de conversões

 Geração de relatórios semanais/mensais

📞 Informações de Contato
Para dúvidas ou sugestões sobre o Lead Flow, documente melhorias e compartilhe!

📄 Licença
Código de uso livre. Adapte conforme necessário para seu negócio.

Última atualização: Março 2026
Versão: 1.0
Status: ✅ Produção
