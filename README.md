# IP-Details

## Description
This program is used to list out the information of multiple public IP Addresses. It displays the type of IP, continent, country, country capital, region, city, latitude, longitude, organization and the ISP. Internet connection is mandatory for this program to execute. Libraries used are requests, json, csv, pandas, os.

## Files Used
1. ip.csv (IP address input file)
2. ip_details.py (Main program)
3. ip_info.csv (Output file)

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

**View [docs](https://docs.google.com/document/d/1YUmSMYsSUedoLNFgHlENzEF24FvgG6kRCrZJ4b2XudM/edit?usp=sharing) for more info**

