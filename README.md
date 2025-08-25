# Case_Cirion_20250825

## Pontos importantes antes de Subir a tabela para o POWER BI:

1 - Visualizar a base em algum banco (Pyhton, SQL etc), para verificar o formato da informações, pois se vier com algum erro solicitar para responsávies a correção necessária

2 - A base veio normalizada no "State", ou seja, é a campo que mostra o último status da operação, e o campo "evento" mostra todo o movimento da base, desde o cadastro da falha até o fechamento, cancelamento ou requisição 

3 - Devemos antes de subir a base fazer as correções necessárias no Power Query, como não teve uma documentação do que deveria ser considerado, fiz algumas premissas:
    
    - Para os cálculos serem mais fidedignos, exclui os chamados cancelados, e requitados, por desconhecimento se entra ou não na análise
    - Os campos ServiceRestoredDate,FailureOrigin são não nulos para a análise
    - Pivotei a tabela no comando no python em anexo, para ter a data exata do tratamento da falha
    - Quando fiz a conta do delta da ServiceRestoredDate pela CreationDate, vi que o MTTR não fazia sentido pois ultrapassava 36 hrs para o reparo, então usei a data do fechamento e a data do operador no site para calcular o MTTR (Premissa que assumi)   

## Power BI

1 - O layout está na cor padrão da Cirion, ou algo próximo, foi utilizado FIGMA para a Capa, e PNG no Power Point para o Background

2 - STAR Schema na construção da Tabela Fato, e as dimensões, além de usar a linguagem M para fazer uma Tabela Calendário para Hierarquia de Datas, este ponto é importante para as boas práticas de mercado

3 - Visão geral: KPIs principais devem partir de cima para baixo em cards (Ex: Total de Falhas no Período, MTTR e % Meta de 4hrs, e na lateral os filtros como (data, origem da falha, empresa, país)

4 - Análise Temporal: Os gráficos na primeira aba mostram um visão ao longo do tempo das falhas (Visão MoM e Trimestral), duas aberturas em barras, e uma tabela, já visando qual Empresa está dentro da Meta

5 - Análise por Empresa e Regional: Está na ultima aba, um gráfico de barras com a linha na meta, mostra qual País e Empresa estão perfomando melhor e para não poluir o gráfico foi feita uma tabela mostrado qual o % está na meta de 4hrs

6 - Visão Diária: Essa aba é importante para acompanhar a operação Real Time, supondo que a base retroalimenta, essa aba mostraria se algum indicador está chegando próxima da meta, poderia ser realizado um gatilho por e-mail (Aqui precisa de e-mail corporativo Microsoft para usar o Power Automate e Publicar o Dashboard), e ainda coloquei um filtro de dia util (considerando o Calendário brasileiro)

## DAX e Linguagem M no Power Query

1 - No DAX, foram feitas fórmulas básicas como count ( contagem de falhas), sum (soma das horas para o mttr), divide (divisão para calcular taxa), filter ( Como e fosse um where do SQL), Calculate (Construção de indicadores calculados), Coalesce (Eliminar um erro de divisão) 

2 - Na linguagem M basicamente subimos uma base bruta e vamos limpando no Power BI (Não é o ideal), além de campos personalizados como o TEMPO_OPERACAO, e a Ultima Data de Atualização (Está não funciona no desktop, pois não temos gatilho, mas deixei no corpo do dashboard, isso mostra quando o dashboard atualiza), e o calculo dos dias uteis




   
