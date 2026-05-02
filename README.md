# Fausto

Estratégias NTSL disponíveis:

## `estrategia_quatro_medias.src`

- 4 médias aritméticas configuráveis por input
- dois períodos de operação configuráveis por input
- venda por retorno contra a tendência de baixa quando o fechamento fica acima da média das máximas
- compra por retorno contra a tendência de alta quando o fechamento fica abaixo da média das mínimas
- saída por toque na média oposta ou por stop configurável em pontos via input, o que acontecer primeiro

## `scalp_reversao_alvo.src`

- scalp por rompimento da máxima ou mínima da vela fechada anterior
- alvo configurável em pontos e quantidade inicial configurável por input
- sem stop fixo
- ao surgir uma vela fechada no sentido oposto, arma reversão no extremo dessa vela com o dobro da quantidade atual
- ao atingir o primeiro alvo do dia, interrompe novas operações até a virada da data
