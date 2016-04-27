#希望用flask作为中介让python和js交互
##Solution
```
Javascript + jQuery:
mydata = {"msg", "Hello Flask."};          // 要传输的数据
$.getJSON('/dataconvector', {              // Flask中获取数据的function的url
        mykey: JSON.stringify(mydata)      // 定义一个keyword, 将数据stringify
    }, function(data) {                    // 从Flask返回的数据
        console.log(data.result);
        $( "#result" ).text(data.result);
    }
);

Python + Flask:
import json                  # Python build-in function
from flask import jsonify    # Flask build-in function

@app.route('/dataconvector')
def dataConvector():
    mydata = json.loads(request.args.get('mykey'))
    mydata['msg'] = "Hello Javascript."
    return jsonify(result=mydata)

```
