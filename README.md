<div>
  <img src="https://raw.githubusercontent.com/GeorgeTelles/georgetelles/f69531ec6b293b5148563588a764c010015d315e/logo_clara.png" alt="logo clara" width="300" style="display: inline-block; vertical-align: top; margin-right: 10px;">
  <img src="https://raw.githubusercontent.com/GeorgeTelles/georgetelles/f69531ec6b293b5148563588a764c010015d315e/logo_dark.png" alt="logo dark" width="300" style="display: inline-block; vertical-align: top;">
</div>

# Extração e Análise de Dividendos com Python

## Introdução

Este projeto em Python visa extrair e analisar informações sobre dividendos e juros sobre capital próprio (JCP) pagos por empresas brasileiras. A análise inclui a obtenção de dados de dividendos e JCP, a decodificação de parâmetros codificados em base64, a comparação de dados obtidos com outras fontes e o calculo do Dividend Yield.

## Teoria

### Dividendos

Os dividendos são a parcela do lucro de uma empresa distribuída aos seus acionistas. 

- **Periodicidade**: Podem ser pagos trimestralmente, semestralmente ou anualmente.
- **Obrigatoriedade**: De acordo com a Lei das Sociedades por Ações (Lei nº 6.404/76), as empresas devem distribuir no mínimo 25% do lucro líquido ajustado, salvo decisão em contrário.
- **Forma de Pagamento**: Podem ser pagos em dinheiro, ações adicionais, ou outras formas.
- **Imposto de Renda**: Isentos de imposto de renda para pessoa física no Brasil.

### Juros sobre Capital Próprio (JCP)

Os JCP são uma alternativa aos dividendos e permitem às empresas deduzirem essa despesa, reduzindo o imposto de renda e a contribuição social sobre o lucro líquido (CSLL).

- **Base Legal**: Regido pela Lei nº 9.249/95.
- **Cálculo**: Limitado a uma taxa de juros definida pela legislação, aplicada sobre o patrimônio líquido da empresa.
- **Tributação**: Sujeito a retenção de imposto de renda na fonte, com alíquota de 15%.
- **Dedutibilidade**: Pode ser abatido do lucro tributável pela empresa.

### Comparação entre Dividendos e JCP

- **Impacto Fiscal para a Empresa**: Dividendos não são dedutíveis; JCP são dedutíveis.
- **Tributação para o Acionista**: Dividendos são isentos; JCP sofre retenção na fonte.
- **Flexibilidade de Uso**: Empresas podem optar por combinar dividendos e JCP conforme estratégia fiscal e financeira.

## O que Você Precisa Saber Sobre as Datas

### Data Com (ou Data de Corte)

- **Data Com**: Último dia para possuir ações e ter direito aos proventos.
- **Data Ex-Dividendo**: Dia seguinte à Data Com, quando as ações são negociadas sem direito aos proventos.
- **Exemplo Prático**: Se a Data Com é 10 de junho, comprar ações até o final do dia 10 garante o direito aos dividendos.

### Resumo das Datas Importantes

- **Data de Declaração**: Data de anúncio dos dividendos ou JCP.
- **Data Com**: Último dia para ter direito aos proventos.
- **Data Ex-Dividendo**: Quando as ações são negociadas sem os proventos.
- **Data de Pagamento**: Quando os dividendos ou JCP são pagos.

## Conceitos Utilizados no Código

### Decodificação e Codificação Base64

A B3 usa codificação base64 para compor URLs de request para obter dados de dividendos:

- **Compactação e Codificação**: Transforma dados binários em uma string ASCII, garantindo segurança e padronização.
- **Segurança e Integridade**: Ofuscação e verificação de integridade dos dados.
- **Facilidade de Manipulação e Transmissão**: Uniformidade e compatibilidade com sistemas de rede e APIs.
- **Encapsulamento de Dados Complexos**: Facilita a transmissão de dados complexos como parâmetros de URL.

## Fonte dos Dados

- [B3 - Empresas Listadas](https://www.b3.com.br/pt_br/produtos-e-servicos/negociacao/renda-variavel/empresas-listadas.htm)
- [Rico - Dividendos](https://riconnect.rico.com.vc/blog/dividendos/)

from base64 import b64decode, b64encode
import pandas as pd
import requests
import seaborn as sns
import matplotlib.pyplot as plt
import yfinance as yf
