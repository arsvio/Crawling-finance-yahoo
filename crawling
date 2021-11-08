### Extract from Yahoo Link ###
for ticker in ticker_list:
    url = 'https://finance.yahoo.com/quote/' + ticker[0]
    session = requests_html.HTMLSession()
    r = session.get(url)
    content = BeautifulSoup(r.content, 'lxml')
    try:
        price = content.select_one('.Mb\(-4px\)').text
        # print(price)
    except IndexError as e:
        price = 0.00
    price = price or "0"
    try:
        price = float(price.replace(',',''))
    except ValueError as e:
        price = 0.00
    time.sleep(1)
    with DBcm.UseDatabase(config) as cursor:
        _SQL = """insert into tickers
                  (ticker, price, company_name, listed_exchange, category)
                  values
                  (%s, %s, %s, %s, %s)"""
        print(ticker[0], price, ticker[1], ticker[2], ticker[3])
        cursor.execute(_SQL, (unidecode.unidecode(ticker[0]), price, unidecode.unidecode(ticker[1]), unidecode.unidecode(ticker[2]), unidecode.unidecode(ticker[3])))
print('completed...')
