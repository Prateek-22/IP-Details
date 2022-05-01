# IP-Details

## Code
```
import requests
import json
import csv
import pandas as pd
import os
import pandas
import time

with open('ip.csv') as input_file:
    ip_reader = csv.reader(input_file, delimiter=' ')

    for row in ip_reader:
        current_ip = row[0]
        request_url = 'https://ipwhois.app/json/' + current_ip
        response = requests.get(request_url)
        result = response.content.decode()

        result = json.loads(result)

        data = [result]
        df = pd.DataFrame.from_dict(data)
        df.to_csv('FINAL.csv', mode='a')

f = open('FINAL.csv')
csv_final = csv.reader(f)

df = pd.read_csv("FINAL.csv", usecols=["ip", "type", "continent", "country", "country_capital", "region", "city", "latitude", "longitude", "org", "isp"])
print(df[::2])
f.close()
os.remove('FINAL.csv')
df[::2].to_csv('ip_info.csv')
```

