import json
import pprint
import requests
import time


# introducing the service to users
def displayIntro():
    print('Welcome to the USD and WON currency API service.')
    print('You can check the latest currency rate (base:EUR).')
    print('Currency rates available: USD, AUD, CAD, PLN, MXN')
    print('Collecting data...')
    time.sleep(3)


displayIntro()  # run displayIntro fuction


def main():
    # set API Endpoint, access key, required parameters
    symbols = 'USD,AUD,CAD,PLN,MXN&format=1'

    mainurl = url + accessKey + '&symbols=' + symbols
    response = requests.get(mainurl)
    response.raise_for_status()  # check for errors

    # load json data
    jsonData = json.loads(response.text)
    pprint.pprint(jsonData)

    varBase = jsonData['base']
    print(varBase)

    varRates = jsonData['rates']
    print(varRates)

    varDate = jsonData['date']
    print(varDate)

    currencylistOption1 = [varBase], [varRates]
    currencylistOption2 = [varBase], [varRates], [varDate]

    # After looking at the pprint results and the documentation, pick out specific data
    print('What information would you want to download? (1: base, rates OR 2: base, rates, time)')
    options = input()

    if options == '1':
        time.sleep(0.5)
        print(currencylistOption1)

    elif options == '2':
        time.sleep(0.5)
        print(currencylistOption2)


def data():
    url = 'http://data.fixer.io/api/latest?access_key='
    accessKey = '4aabd2e275cac470084d2e76a5b03ece'
    symbols = 'USD,AUD,CAD,PLN,MXN&format=1'

    mainurl = url + accessKey + '&symbols=' + symbols
    response = requests.get(mainurl)
    response.raise_for_status()  # check for errors

    jsonData = json.loads(response.text)
    print(pprint.pprint(jsonData))


def result(currencylistOption1):
    #get and save txt.
    time.sleep(2)
    print('Saving your data as txt file...')
    f = open('Currencyratedata.txt', 'w')
    f.write(currencylistOption1)
    f.close()
    #f = open('Currencyratedata.txt')
    #content = f.read()
    #f.close()
    #print(content)

    print('Result in text file. File name: CurrencyRateData.txt.')
    return


main()      #run main function
result()

#g = data(jsonData)


#the end. Ask the user for run program again.
print('Would you like to run the program again? (y: yes, n: no)')
runAgain = input()
while runAgain == 'yes' or 'y':
    displayIntro()
    main()
    break
