Atue como um especialista em N8N.

Crie uma automação para notificar clientes sobre cobranças pendentes e próximas do vencimento.

Público:
Equipe financeira de uma empresa que precisa reduzir a inadimplência e manter os clientes informados de forma personalizada.

Ferramentas envolvidas:
API de cobranças (via HTTP Request), Google Sheets (lista de clientes) e Gmail (envio de e-mails em formato HTML).

Fluxo:
1. Iniciar o workflow com um Schedule Trigger diário.
2. Consultar a API de cobranças usando o parâmetro status=pending, para buscar apenas cobranças pendentes.
3. Buscar a lista de clientes no Google Sheets.
4. Se os dados vierem em arrays, usar o nó Split Out para separar cada cliente ou cobrança em itens individuais.
5. Usar o nó Merge no modo Combine para unir cada cobrança ao seu cliente, associando campos com nomes diferentes, mas com o mesmo significado (ex.: "ID" na lista de clientes e "Customer" na lista de cobranças). Manter apenas os registros que tenham correspondência nos dois inputs.
6. Calcular os dias para o vencimento e usar um nó IF para decidir quem deve ser notificado.
7. Usar o Loop Over Items para percorrer cada cliente.
8. Enviar um e-mail em formato HTML com dados dinâmicos do item atual (nome do cliente, valor e data de vencimento).

Regras:
- Buscar somente cobranças com status=pending.
- Não enviar aviso de atraso a clientes com pagamento automático no cartão, a menos que o pagamento não seja processado e haja atraso.
- Usar dados dinâmicos do item atual do loop, sem referenciar diretamente um nó anterior.
- Personalizar o e-mail com o nome do cliente e a data de vencimento, para aumentar a relevância e evitar que pareça spam.
- Se for necessário enviar SMS além do e-mail, usar nós separados para cada canal.
- Ignorar registros sem e-mail válido.
