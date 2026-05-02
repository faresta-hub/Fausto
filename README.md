# Fausto

Estratégia NTSL adicionada em `estrategia_quatro_medias.src`.

Resumo:
- 4 médias aritméticas configuráveis por input
- filtro de horário configurável, iniciando em 16:00-17:00
- venda por retorno contra a tendência de baixa quando o fechamento fica acima da média das máximas
- compra por retorno contra a tendência de alta quando o fechamento fica abaixo da média das mínimas
- saída por toque na média oposta ou por stop configurável em pontos via input, o que acontecer primeiro
