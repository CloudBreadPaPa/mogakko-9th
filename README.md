# 모각코x모두 아홉번째 모임 - 발표자료
## C#, node.js + (Python) 을 이용한 Azure Machine Learning API 데모 코드

이 Repository는 모각코x모두 아홉번째 모임 발표에 사용된 demo 코드.
발표에 대한 자료와 내용은 모두 모각코 facebook 모임에서 보실 수 있습니다. 
https://www.facebook.com/events/527785940755737/

### C#을 이용한 Visual Studio 실행 절차
mogakko-9th\cs\mokakko-9th-dw-demo 폴더에서 프로젝트 실행
코드의 API KKey를 자신의 Azure ML API Key로 수정

```
...
const string apiKey = "API Key"; // Azure ML이 제공하는 API Key
...
client.BaseAddress = new Uri("Azure ML이 제공하는 API URL");
...
```

### node.js로 ML API를 호출하는 절차
app.js 파일의 API Key를 자신의 API Key로 수정

```
...
var host = 'asiasoutheast.services.azureml.net'	//제공하는 HOST 경로
var path = 'HOST 이후 URL Path 정보'
...
var api_key = 'API Key 정보'
...
```

node.js로 Azure ML을 call 예제 링크 :
https://blogs.msdn.microsoft.com/bigdatasupport/2016/02/18/how-to-call-a-azure-machine-learning-web-service-from-nodejs/

node reqeust package를 이용하면 더 쉽게 node에서 Azure ML을 호출 가능할 것으로 예상됨.
참고링크 : https://github.com/request/request

### Python을 이용한 Azure ML 호출 코드
Python을 호출하기 위한 데모
기본 code는 Python 2.7.x 기준. 아래 코드 데모는 아마도 한글로 인해 unicode 처리가 필요할 수 있음.

```
import urllib2
# If you are using Python 3+, import urllib instead of urllib2

import json 


data =  {

        "Inputs": {

                "input1":
                {
                    "ColumnNames": ["idx", "나이", "프로모션참여수", "식별자", "일평균게임플레이분", "90일내아이템구매수", "게임레벨범위", "보유크리스탈", "유입경로", "인종", "성별", "가입코드", "구매번호", "주당접속수", "가입국가", "이탈여부"],
                    "Values": [ [ "0", "0", "0", "0", "0", "0", "0", "0", "value", "value", "value", "0", "0", "0", "value", "value" ], [ "0", "0", "0", "0", "0", "0", "0", "0", "value", "value", "value", "0", "0", "0", "value", "value" ], ]
                },        },
            "GlobalParameters": {
}
    }

body = str.encode(json.dumps(data))

url = 'AzureML이 제공하는 URL'
api_key = 'AzureML이 제공하는 APIKey' # Replace this with the API key for the web service
headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}

req = urllib2.Request(url, body, headers) 

try:
    response = urllib2.urlopen(req)

    # If you are using Python 3+, replace urllib2 with urllib.request in the above code:
    # req = urllib.request.Request(url, body, headers) 
    # response = urllib.request.urlopen(req)

    result = response.read()
    print(result) 
except urllib2.HTTPError, error:
    print("The request failed with status code: " + str(error.code))

    # Print the headers - they include the requert ID and the timestamp, which are useful for debugging the failure
    print(error.info())

    print(json.loads(error.read()))

```

마찬가지로, API Key 변수를 자신의 Key로 변경하고 수행 해야 함.

```
...
url = 'AzureML이 제공하는 URL'
api_key = 'AzureML이 제공하는 APIKey' # Replace this with the API key for the web service
...
```

이부분을 변경하고 수행

문서의 끝
