# CODE

import requests 

import pandas as pd

from bs4 import BeautifulSoup


product_name=[]

prices=[]

description=[]



for i in range(2,12):

    url= "https://flipkart.com/search?q=laptops+under+60k&amp;as=on&amp;as-show=on&amp;otracker=AS_Query_OrganicAutoSuggest_7_14_na_na_ps&amp;otracker1=AS_Query_OrganicAutoSuggest_7_14_na_na_ps&amp;as-pos=7&amp;as-type=RECENT&amp;suggestionId=laptops+under+60k&amp;requestId=5402f762-31cc-416e-ae97-362b034030d6&amp;as-searchtext=laptops+under+&amp;page="+str(i)
    
    r= requests.get(url)
    
    soup= BeautifulSoup(r.text,"lxml")

    box= soup.find("div",class_="_1YokD2 _3Mn1Gg")


    names= box.find_all("div",class_= "_4rR01T")


    for i in names:
        
        name= i.text
        
        product_name.append(name)


    price=box.find_all("div",class_="_30jeq3 _1_WHN1")

    for i in price:
    
        p=i.text
        
        prices.append(p)
    
    

    desc= box.find_all("ul",class_="_1xgFaf")
    

    for i in desc:
    
        d=i.text
        
        description.append(d)
    
data=pd.DataFrame({"Product Name":product_name,"Price":prices,"Description":description})

data.to_csv('laptop_under_60k.csv')

