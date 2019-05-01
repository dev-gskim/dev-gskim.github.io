---
title: "address to elasticsearch
date: 2019-04-30 19:00:00 +0900
categories: python
---

## 주소데이터를 elasticsearch 에 저장

* 행정안전부(https://www.mois.go.kr) 에서 [주민등록 및 인감]을 조회
* 주민등록주소코드 변경내역 게시물에서 첨부파일(주소)을 다운
* 행정동 코드 xlsx를 utf-8 형태의 csv로 저장
* python 코드로 es에 저장

~~~ python
import sys
import os

from elasticsearch import Elasticsearch
import requests 
import json
import csv

es = None
es_index = 'addr_info'
es_doc = 'address'

host_ip = '192.168.3.22'
host_port = 9200

addr_list = []

def loadAddressFromCsv(csvFileName):
  if not os.path.exists(csvFileName):
    print ("file not exists")
    return False

  lineCnt = 0
  addr_list.clear()

  with open(csvFileName, 'r', encoding='utf-8') as csv_addr:
    h_csv = csv.reader(csv_addr, delimiter=',')
    for row in h_csv:
      es_data_body = {
        "regDate" : '20190415', 
        "admCd": row[0], 
        "siNm" : row[1], 
        "sggNm": row[2], 
        "liNm" : row[3], 
        "rn"   : "", 
        "lat"  : 0, 
        "lon"  : 0
      }
      addr_list.append(es_data_body)
      lineCnt += 1

  print ("complete line :", lineCnt)
  #print (addr_list)

  return True

# elasticsearch post
def espost(es_uri, es_data):
  #print (es_uri, es_data)
  headers = {'Content-Type': 'application/json; charset=utf-8'}
  res = requests.post(es_uri, headers=headers, data=json.dumps(es_data), timeout=3) # timeout 3 second
  '''
  if res.status_code == 201:
    print("create ok")
  elif res.status_code == 200:
    print("update ok")
  else:
    print("error")
  '''
  return True

def addr_to_es():
  base_uri = 'http://{0}:{1}/{2}/{3}/'.format(host_ip, host_port, es_index, es_doc)
  
  print ("sending address...")
  for addr in addr_list:
    send_uri = base_uri + addr["admCd"]
    send_addr = {
      "regDate": addr["regDate"]
      ,"admCd" : addr["admCd"]
      ,"sggNm" : addr["sggNm"]
      ,"siNm"  : addr["siNm"]
      ,"liNm"  : addr["liNm"]
    }
    espost(send_uri, send_addr)

  print ("complete send")
  
# connect elasticsearch 
def es_conn():
  try:
    es = Elasticsearch([host_ip], port=host_port)
    print ("Connected", es.info())
  except Exception as ex:
    print ("Error:", ex)

if __name__ == "__main__":
  print ('hi')
  if len(sys.argv) <= 1:
    print('please file name')
    sys.exit(0)

  es_conn()
  if loadAddressFromCsv(sys.argv[1]):
    addr_to_es()


~~~
