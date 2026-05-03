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

## `scalp_abertura.src`

- scalp das primeiras velas do dia (mini índice), explorando a volatilidade da abertura do pregão
- analisa cada candle fechado a partir de `HoraInicioPregao` (padrão 9h00); se positivo, arma `BuyStop` na máxima; se negativo, arma `SellShortStop` na mínima
- se a ordem não disparar no candle seguinte, é cancelada e rearmada com os extremos do novo candle
- quando a ordem dispara, coloca alvo em `AlvoPontos` pontos via `SellShortLimit` / `BuyToCoverLimit`; ao atingir o alvo, para de operar no dia
- se fechar um candle de direção oposta sem ter atingido o alvo, fecha a posição e arma nova entrada com o dobro da quantidade (virada de mão / martingale)
- número de viradas permitidas limitado por `MaxViradas` (padrão 3); ao esgotar as viradas, encerra e não opera mais no dia
- novos sinais de entrada são gerados apenas até `HoraFimSinais` (padrão 9h30), mas posições abertas continuam sendo gerenciadas após esse horário
- `AlvoPontos`, `QuantidadeInicial`, `MaxViradas`, `HoraInicioPregao` e `HoraFimSinais` são configuráveis por input
- todo o estado é resetado na virada do dia

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
