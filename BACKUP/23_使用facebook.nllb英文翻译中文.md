# [使用facebook nllb英文翻译中文](https://github.com/cutepig123/gitblog/issues/23)

测了一下。效果一般般。感觉比google翻译差

```python

# https://huggingface.co/spaces/Geonmo/nllb-translation-demo
import requests
import time

def PostData(url, json_data):
    resp = requests.post(url,json=json_data)
    resp_json = resp.json()
    return resp_json

text = '''


By default, OpenTracing doesn't log automatically into span logs, only important messages that Jaeger feels it needs to be logged and is needed for tracing would be there :). The idea is to separate responsibilities between Tracing and Log management, Check this GitHub discussion.

An alternative would be to use centralized log management and print traceId & spanId into your logs for troubleshooting and correlating logs and tracing.

'''
request_json = {"fn_index":0,"data":["English","Chinese (Simplified)",text],"action":"predict","session_hash":"un6x6o8iojq"}
resp = requests.post('https://geonmo-nllb-translation-demo.hf.space/api/queue/push/',json=request_json)
resp_json = resp.json()
hash = resp_json['hash']
print(resp_json)

while True:
    url = 'https://geonmo-nllb-translation-demo.hf.space/api/queue/status/'
    request_json = {"hash":hash}
    resp_json = requests.post(url,json=request_json).json()
    # {"status":"COMPLETE","data":{"data":[{"inference_time":0.7774190902709961,"source":"eng_Latn","target":"zho_Hans","result":"你好世界"}],"duration":0.7777302265167236,"average_duration":3.264024568158527}}
    print (resp_json)
    if resp_json['status']=='COMPLETE':
        break
    time.sleep(1)

```

Output

```
PS C:\JS\Desktop> & c:/Users/aeejshe/AppData/Local/anaconda3/python.exe c:/JS/Desktop/test_nllb.py
{'hash': '16908fcfa6dc496d8de8bcfbef8e0fba', 'queue_position': 0}
{'status': 'PENDING', 'data': None}
{'status': 'PENDING', 'data': None}
{'status': 'PENDING', 'data': None}
{'status': 'PENDING', 'data': None}
{'status': 'PENDING', 'data': None}
{'status': 'PENDING', 'data': None}
{'status': 'PENDING', 'data': None}
{'status': 'PENDING', 'data': None}
{'status': 'PENDING', 'data': None}
{'status': 'PENDING', 'data': None}
{'status': 'PENDING', 'data': None}
{'status': 'COMPLETE', 'data': {'data': [{'inference_time': 21.45255422592163, 'source': 'eng_Latn', 'target': 'zho_Hans', 'result': '默认情况下,OpenTracing不会自动 
登录到跨度日志中,只有Jaeger认为需要登录的重要消息,并且需要追踪的信息将会存在:). 想法是分开追踪和日志管理之间的责任,查看这篇GitHub讨论. 另一个选择是使用集中记录管理, 
并在您的日志中打印traceId & spanId来解决故障,并对相关日志和追踪. '}], 'duration': 21.45286989212036, 'average_duration': 3.95068706035614}}
PS C:\JS\Desktop> ^N
```
