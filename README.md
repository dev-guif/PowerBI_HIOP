# [Em construção] - BI HIOP
Dashboard em Power BI para o Hospital IOP, taxa de ocupação e centro cirúrgico.
Menu, múltiplas páginas, conexão e consulta direto com banco Oracle Tasy (sistema de gestão hospitalar Philips),  visual feito por mim, metas mensais e diárias, quantitativos e filtros de anos anteriores, filtro de data personalizado, filtro de convênio, gráfico comparativo entre convênios, data de última atualização da base e  tabela Date para melhor fazer os comparativos que envolvem datas.
Segue minhas métricas:
- Total Mes Atual = CALCULATE([Total Cirurgias],Calendario[Ano] = 2022, LASTNONBLANK(Calendario[Mês], 1))
  Calcula o total de cirurgias do mês atual.
- Total Hoje = LASTNONBLANKVALUE (Calendario[Data], [Total 2022])
  Calcula o total de cirurgias hoje.
- Total Cirurgias = COUNTROWS(base_hiop)
  Calcula o total de cirurgias que temos disponível na base.
- Total 2022 = CALCULATE([Total Cirurgias],Calendario[Ano] = 2020)
  Calcula o total de cirurgias por ano, existem outras 3 métricas para os anos de 2019, 2020 e 2021 seguindo a mesma lógica.
- Meta Cirurgias Mensal = CALCULATE([Total Mes Atual], DATEADD(Calendario[Data],-1, MONTH))
  Calcula o quantitativo de cirurgias do mês anterior, minha meta a ser batida no mês atual (usado no KPI).
- hoje exec = CALCULATE([Total Hoje], FILTER(base_hiop, base_hiop[DS_STATUS_AGENDA]="Executada"))
  Calcula as cirurgias executadas hoje.
- Cirurgias do Mes Anterior = CALCULATE([Total Cirurgias],DATEADD(Calendario[Data],-1,YEAR))
  Calcula as cirurgias do mês anterior.
