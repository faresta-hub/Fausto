# Fausto

Estratégias NTSL para automação de operações.

## Arquivos

- `abertura_1min.ntsl`: estratégia para gráfico de 1 minuto focada no primeiro movimento do pregão.

## Estratégia `abertura_1min.ntsl`

Faz entrada a mercado na direção de candles cujo corpo é maior que cada um dos pavios individualmente, respeitando uma janela inicial do pregão e um limite de operações por dia.

### Inputs principais

- `horarioInicio(900)`: início da janela de entradas.
- `horarioFimEntradas(930)`: fim da janela de entradas.
- `alvoPontos(100)`: alvo em pontos.
- `stopPontos(100)`: stop em pontos.
- `numeroOperacoesDia(1)`: máximo de operações por dia.
