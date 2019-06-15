import os
from bs4 import BeautifulSoup
from __future__ import division
import nltk, re, pprint
import nltk
from nltk import corpus
from urllib import urlopen
import pandas as pd
# Access law firm webpage

law_firm_list = 'https://www.law.com/law-firms/?firm=&ranking=Nlj500Rank&location='
lf_raw = urlopen(law_firm_list).read()

#Attempt 1 - using regex

#Fetching law firm URLs
names_matchlist = []
names_matchlist = re.findall(r'<h4(.*)<\/h4>',lf_raw)
names_matchlist_1 = map(lambda x: str.replace(
        str(re.findall(r'href=\"(.*)\">',x)),"[","").replace("]","").replace("'","").replace("\"",""),
        names_matchlist)
names_matchlist_1 = names_matchlist_1[1:300]

#Open a sample URL
firm_URL = 'https://www.law.com' + names_matchlist_1[1]

# Looping to retrieve years, revenue and headcount data

for i in range(1,301):
    print("Firm no: ",i)
    #open URL
    firm_URL = 'https://www.law.com' + names_matchlist_1[i]
    firm_text = urlopen(firm_URL).read()   

    #fetch name of law firm
    name = str(re.findall(r'<title>(.*) \|',firm_text)).replace('[','').replace(']','').replace("'","")
    print(name)
    
    # X-Axis data - years
    years_data = str(re.findall(r'categories: \[(.*)\]\,(\s)+crosshair',firm_text))
    years_data = str(re.findall(r'\"(.*)\"',years_data)).replace('[\"','').replace('\"]','').replace('\'','').split(",")
    print(years_data)
    
    # Y-Axis data - Revenue
    revenue_tl = str(re.findall(r'\'Revenue\'(.*?)\]',firm_text))
    revenue_tl = str(re.findall(r'data\: \[(.*?)\]',revenue_tl)).replace('[\'','').replace('\"\']','').split(',')
    print(revenue_tl)

    # Y-Axis data - Headcount
    hcount_tl = str(re.findall(r'\'Headcount\'(.*?)\]',firm_text))
    hcount_tl = str(re.findall(r'data\: \[(.*?)\]',hcount_tl)).replace('[\'','').replace('\"\']','').split(',')
    print(hcount_tl)
