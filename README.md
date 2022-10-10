# Projeto - Buscando informações na web automaticamente

Neste projeto, foi desenvolvido um script, com o pacote Selenium, no Python, que navega na internet, extrai a cotação de algumas moedas e salva em uma base de dados, com a data e hora. 

Os princípios para o desenvolvimento deste script poderiam ser utilizados para extrair quaisquer informações da internet e atualizar uma base de dados, automaticamente.

Há uma forma de realizar essa mesma consulta, sem a necessidade da abertura de um browser, porém, por querer demonstrar visualmente que o código está rodando, optei por essa forma de consulta. 

1. Ferramentas utilizadas
    1. Python
    2. Bibliotecas (Selenium, Pandas)
    3. VSCode (Jupyter Extension)
    4. Base de dados CSV
2. Passos a serem seguidos
    1. Importar as bibliotecas
    2. Importar a base de dados e verificar os tipos de informação
    3. Criar as funções, através do pacote Selenium, que irão extrair as informações de páginas web.
    4. Atualizar a base de dados e salvar.
3. Como funciona a busca de informações com o pacote Selenium?

Ao executar o comando: 

```python
browser = webdriver.Edge()
browser.get("https://www.google.com/")
```

O navegador Microsoft Edge será aberto e o site [google.com](http://google.com) será aberto, em seguida.

Para identificar a caixa de busca, será necessário clicar com o botão direito na página e no menu aberto, clicar em “Inspecionar”.

<div align="center">
<img src="https://user-images.githubusercontent.com/110427400/194936212-1e02bebe-6f78-46d8-b227-f1c97e776c81.png" width="300px" />
</div>

Um menu de inspeção será aberto e deverá clicar no botão do canto superior esquerdo.

<div align="center">
<img src="https://user-images.githubusercontent.com/110427400/194936754-457b4afc-882e-4c18-8c40-5fc437416e7b.png" width="300px" />
</div>

Após clicar no botão, mova o mouse para cima da barra de busca do google e clique.

<div align="center">
<img src="https://user-images.githubusercontent.com/110427400/194936866-3f5f02e6-8cb4-4fe5-93e3-d4f4403ce543.png" width="600px" />
</div>

Dessa forma, será destacado no código fonte da página, a seção referente à barra de busca.

Clicando com o botão direito sobre a parte destacada do código, surgirá um menu. Neste menu, clique em copiar o XPATH.

<div align="center">
<img src="https://user-images.githubusercontent.com/110427400/194936963-8aa37f1a-be95-4ed3-9da4-8a974963b1b9.png" width="300px" />
</div>

Com o XPATH copiado, é só utilizar a seguinte função, colando-o entre aspas:

```python
browser.find_element(By.XPATH,
                            '/html/body/div[1]/div[3]/form/div[1]/div[1]/div[1]/div/div[2]/input').send_keys('cotação dólar')
browser.find_element(By.XPATH,
                            '/html/body/div[1]/div[3]/form/div[1]/div[1]/div[1]/div/div[2]/input').send_keys(Keys.ENTER)
```

Dessa forma, o Selenium clicará sobre a barra de busca e enviará uma string pela função “send_keys”. Após isso, utilizar novamente a função “send_keys” para dar Enter.

Ao ser redirecionado para a página correspondente ao termo pesquisado no passo anterior, utilizar a mesma ferramenta de inspeção para se extrair o XPATH da informação desejada, neste caso, a cotação do dólar.

<div align="center">
<img src="https://user-images.githubusercontent.com/110427400/194937049-76d9a6d1-3b0e-4ee8-afbf-b04e335668ac.png" width="300px" />
</div>

Com o XPATH copiado, utilizar a seguinte função: 

```python
cotacao = browser.find_element(By.XPATH,
                            '//*[@id="knowledge-currency__updatable-data-column"]/div[3]/div/div[2]/input').get_attribute('value')
```

Com esta função, o “value” do elemento será copiado e então, é só o salvar na base de dados.

Enfim, um termo foi pesquisado na internet, um valor alvo foi localizado e extraído da página web e inserido em uma base de dados. 

Pesquisar a cotação de moedas, extrair o valor de uma página web e atualizar uma base de dados foi só um exemplo da utilização desta ferramenta. Existe uma infinidade de casos em que essa ferramenta poderia ser útil.
