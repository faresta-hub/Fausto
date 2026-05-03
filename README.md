# Fausto

Estratégias NTSL disponíveis:

## `breakout_candle_direcional.src`

- estratégia mínima baseada apenas na direção do candle já fechado
- se o candle anterior fechar positivo, arma `BuyStop` na máxima dele
- se o candle anterior fechar negativo, arma `SellShortStop` na mínima dele
- ao entrar comprado, mantém alvo por `SellShortLimit` em `BuyPrice + AlvoPontos`
- ao entrar vendido, mantém alvo por `BuyToCoverLimit` em `SellPrice - AlvoPontos`
- `AlvoPontos` e `Quantidade` são configuráveis por input
- sem stop fixo, sem martingale e sem trava diária

## `estrategia_quatro_medias.src`

- 4 médias aritméticas configuráveis por input
- dois períodos de operação configuráveis por input
- venda por retorno contra a tendência de baixa quando o fechamento fica acima da média das máximas
- compra por retorno contra a tendência de alta quando o fechamento fica abaixo da média das mínimas
- saída por toque na média oposta ou por stop configurável em pontos via input, o que acontecer primeiro

## `scalp_reversao_alvo.src`

- scalp com ordens stop armadas na máxima ou mínima do candle que acabou de fechar, sem atraso de um candle
- alvo configurável em pontos, quantidade inicial configurável por input e teto de quantidade por `MaxQuantidade`
- sem stop fixo
- o alvo é mantido como ordem limite enquanto a posição estiver aberta, evitando esperar a próxima vela para encerrar no backtest
- se a entrada não disparar no candle seguinte, a ordem pendente é cancelada e rearmada usando a máxima ou mínima do último candle já fechado
- se houver posição aberta e fechar um candle na direção oposta, a estratégia fecha a posição a mercado e arma nova entrada stop no extremo desse candle já fechado
- se o fechamento por reversão ocorrer com prejuízo, a próxima entrada usa o dobro da quantidade atual, respeitando `MaxQuantidade`
- a quantidade é resetada para `QuantidadeInicial` na virada da data
- ao atingir o primeiro alvo vencedor do dia, interrompe novas operações até a virada da data
