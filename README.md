# exports-complexity

Os dados da comex para as exportações dos estados brasileiros em frequência anual foram importados e uma estatística como proxy para complexidade econômica ([Mealy et al. 2018](https://oms-inet.files.svdcdn.com/staging/files/main_feb4.pdf)) e variedade da economia de cada estado foi proposta e calculada. A estatística é uma mistura da entropia de Shannon com a ideia da transformação *tf-idf* feita em trabalhos de processamento de linguagem natural ([Blei, 2003](https://www.jmlr.org/papers/volume3/blei03a/blei03a.pdf)). A fórmula é a seguinte: 

$$I(j,t) = -\sum^{n}_{i=1}p(i,j,t)(ln(p(i,j,t)) + ln(f(i,t)))$$

Onde $i$ é o produto classificado pelo NCM, $j$ é o estado e $t$ é o período. $p(i,j,t)$ é então a frequência do produto $i$ na pauta de exportações do estado $j$ no ano $t$. Similarmente, $f$ é a frequência que o produto é exportado por qualquer estado. $ln(x)$ é o logaritmo natural. A ideia é de que quanto mais um produto é frequentemente exportado por um estado  (medido por $p$) menos diversificada é sua pauta de exportações. Como $p<1$, temos que $ln(p) < 0$. Considerando o sinal à esquerda do somatório, temos que $-ln(p) = ln\left(\frac{1}{p}\right)$. Dessa forma, $-ln(p)$ é uma função decrescente em $p$ e, portanto, quanto menos frequente for o produto, maior é o valor de $-ln(p)$. Simlarmente, $f$ entra no cálculo do índice por ser uma proxy de quão raro o produto é entre os estados. Assim, se o estado estiver exportando produtos que são pouco exportados pelos outros estados, isso serve de proxy para indicar que ele possui uma sofisticação produtiva e é capaz de produzir itens mais raros. O índice é então utilizado para estimar uma regressão de dados em painel com efeitos fixos e efeitos de tempo com a renda per capita servindo de variável endógena. O coeficiente estimado para o índice é positivo e extremamente significativo, apesar de o $R^2$ ser bem baixo.

Fontes dos dados: 

[COMEX](https://comexstat.mdic.gov.br/pt/geral)

[ipeadata](http://www.ipeadata.gov.br/Default.aspx)
