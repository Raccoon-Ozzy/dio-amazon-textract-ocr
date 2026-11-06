# Transcrição de Imagens em Texto com Amazon Textract

Projeto desenvolvido durante o bootcamp **Nublify - Primeiros passos em IA e Cloud** da [DIO](https://dio.me).

---

## Visão Geral do Projeto
O objetivo deste projeto é explorar o **Amazon Textract**, um serviço de aprendizado de máquina (Machine Learning) da AWS projetado para extrair automaticamente texto, formulários e dados estruturados de imagens e documentos digitalizados.

Diferente de um OCR (Reconhecimento Óptico de Caracteres) tradicional, o Textract vai além de identificar caracteres isolados: ele compreende o contexto de tabelas, formulários e a relação entre campos e valores (Key-Value pairs).

---

## Fluxo de Funcionamento
1. **Entrada de Dados:** Envio de imagens (PNG, JPEG) ou documentos (PDF) contendo textos impressos ou manuscritos.
2. **Processamento pelo Textract:**
   - Detecção de texto simples (`DetectDocumentText`).
   - Análise de formulários e tabelas estruturadas (`AnalyzeDocument`).
3. **Extração e Estruturação:** Retorno dos dados em formato estruturado (JSON), organizando os dados em blocos de páginas, linhas e palavras com seus respectivos níveis de confiança.
4. **Aplicação Prática:** Os dados extraídos podem ser integrados a bancos de dados, fluxos de automação ou painéis internos.

---

## Exemplo de Implementação com Python (Boto3)

Abaixo está o exemplo conceitual de como o serviço é consumido via código utilizando a biblioteca oficial da AWS (`boto3`):

```python
import boto3

# Inicializa o cliente do Textract
client = boto3.client('textract', region_name='us-east-1')

# Abre a imagem localmente
with open("documento_exemplo.png", "rb") as document:
    response = client.detect_document_text(
        Document={'Bytes': document.read()}
    )

# Exibe o texto detectado
for item in response["Blocks"]:
    if item["BlockType"] == "LINE":
        print(f"Texto detectado: {item['Text']} (Confiança: {item['Confidence']:.2f}%)")
```

---

## Casos de Uso no Mercado
- **Digitalização de Notas Fiscais e Recibos:** Automatização de relatórios financeiros e reembolso de despesas.
- **Validação de Documentos de Identidade (KYC):** Leitura automática de RG, CNH e comprovantes de residência em bancos digitais e fintechs.
- **Processamento de Contratos e Jurídico:** Indexação de cláusulas e extração rápida de termos contratuais.

---

## Insights e Aprendizados
- **OCR Tradicional vs. IA:** O Textract economiza horas de desenvolvimento ao entregar dados já contextualizados em chaves e valores, sem depender de regras rígidas de posicionamento.
- **Governança e Cloud:** O gerenciamento de contas, credenciais IAM e configurações de billing são etapas essenciais para a operação segura e contínua de serviços em nuvem.
