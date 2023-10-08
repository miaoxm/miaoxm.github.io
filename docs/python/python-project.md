[70个python练手项目合集-【尚学堂·百战程序员】](https://www.bilibili.com/video/BV15d4y1q7Zt/?p=3&vd_source=a81ac3671d3f64b919cffe24115c7079)

# NBA球员列表

```python
# pip install requests
import requests
# pip install lxml
from lxml import etree

url = 'https://nba.hupu.com/stats/players'
headers = {'user-agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36'}

resp = requests.get(url, headers = headers)
# 使用xpath
e = etree.HTML(resp.text)

# 使用xpath表达式过滤table标签的class为players_table
nums = e.xpath('//table[@class="players_table"]//tr/td[1]/text()')
names = e.xpath('//table[@class="players_table"]//tr/td[2]/a/text()')
teams = e.xpath('//table[@class="players_table"]//tr/td[3]/a/text()')
scores = e.xpath('//table[@class="players_table"]//tr/td[4]/text()')

# 保存到nba.txt文件中
with.open('nba.txt','w',encoding='utf-8') as f: 
    for num,name,team,score in zip(nums,names,teams,scores):
        f.write(f'排名：{num} 姓名：{name} 球队：{team} 得分：{score}\n')
```

# Demo螺旋线

```python
import turtle
t = turtle.Pen()
for x in range(360):
    t.forward(x)
    t.left(59)
```

# 批量获取王者荣耀皮肤

```python
import os
# pip install requests ctrl + ~
import requests

# pip install lxml
from lxml import etree
from time import sleep

headers = {'user-agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36'}


hero_list_url = 'https://pvp.qq.com/web201605/js/herolist.json'
hero_list_resp = requests.get(hero_list_url, headers = headers)
for h in hero_list_resp.json():
    ename = h.get('ename')
    cname = h.get('cname')
    skin_name = h.get('skin_name')
    
    if not os.path.exists(cname):
        os.makedirs(cname)
        
	# 爬取单个英雄的皮肤
    hero_info_url = 'https://pvp.qq.com/web201605/herodetail/{ename}.shtml'
    hero_info_resp = requests.get(hero_info_url, headers = headers)
    hero_info_resp.encoding = 'gbk'
    e = etree.HTML(hero_info_resp.text)
    names = e.xpath('//ul[@class="pic-pf-list pic-pf-list3"]/@data-imgname')[0]
    names = [name[0:name.index('&')] for name in names.split('|')]

    for i,n in enumerate(names):
        resp = requests.get(f'https://game.gtimg.cn/images/yxzj/img201606/skin/hero-info/{ename}/{ename}-bigskin-{i+1}.jpg', headers = headers)
        with open(f'{cname}/{n}.jpg', 'wb') as f:
            f.write(resp.content)
            print(f'已下载：{n}的皮肤')
            sleep(1)
```

# 抽奖系统

> choujiang/app.py

```python
# 让我们的电脑支持服务访问
# 需要一个web框架
# pip install Flask
from flask import Flask,render_template
from random import randint


app = Flask(__name__)

heros = [‘黑暗之女’,‘狂战士’,‘正义巨像’,‘卡牌大师’,‘德邦总管’,‘无畏战车’,‘诡术妖姬’,‘猩红收割者’,‘远古恐惧’,‘正义天使’,‘无极剑圣’,‘牛头酋长’,‘符文法师’,‘亡灵战神’,‘战争女神’,‘众星之子']

@app.route('/index')
def index():
    return render_template('index.html', heros = heros)
         
@app.route('/luckyDog')
def luckyDog():
     num = randint(0, len(heros)-1)
     return render_template('index.html', heros = heros, hero = heros[num])
app,run(debug=True)
```

> choujiang/templates/index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
	{{ heros }}<br/>
    <a href="/luckyDog">随机抽取</a><br/>
    您抽到了：{{ hero }}
</body>
</html>
```

# 点赞系统

> dianzan/app.py

```python
# pip install flask
from flask import Flask,render_template,request

app = Flask(__name__)

data = [
    {'id': 0, 'name': '中秋节', 'num': 0},
    {'id': 1, 'name': '春节', 'num': 0},
    {'id': 2, 'name': '清明节', 'num': 0}
]

@app.route('/index')
def index():
    return render_template('index.html', data = data)

@app.route('/dianzan')
def dianzan():
    id = request.args.get('id')
    data[int(id)]['num'] += 1
    return render_template('index.html', data = data)   

app.run(debug=True)
```

> dianzan/templates/index/html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <h1>
        这是一个点赞系统
    </h1>
    <table border=“1”>
        <tr>
        	<td>ID</td>
            <td>节假日</td>
            <td>点赞数</td>
            <td>操作</td>
        </tr>
        {% for i in data %}
        <tr>
            <td>{{ i.id }}</td>
            <td>{{ i.name }}</td>
            <td>{{ i.num }}</td>
        	<td>
                <a href="/dianzan?id={{ i.id }}">点赞</a>
            </td>
        </tr>
        {% endfor %}
    </table>
</body>
</html>
```

# 查询工具

```python
# pip install Flask
from flask import Flask,render_template
import requests

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/search_phone')
def search_phone():
    phone = request.args.get('phone')
    data = get_mobile(phone)
    retune '<br/>'.jion(data)

def get_mobile(phone):
    url = f'https://www.ip138.com/mobile.asp?mobile={phone}&action=mobile'
    headers = {'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36'}
    resp = requests.get(url, headers = headers)
    resp.encoding='utf-8'
    e = etree.HTML(resp.text)
    datas = e.xpath('//tr/td[2]/span/text()')
    return datas

app.run(debug=True)
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <form action="/search_phone" method="get">
        手机号：<input type=“text” name="phone" id=""/>
        <input type="submit" value="查询s
    </form>
</body>
</html>
```

# 登录系统

```python
# pip install flask
from flask import Flask,render_template,request

app = Flask(__name__)

@app.route('/login')
def login():
    return render_template('login.html')

@app.route('/index')
def index():
    uname = request.args.get('uname')
    # 判断用户名是否正确
    return f'主页！！！欢迎登录{uname}'


app.run(debug=True)
```

> login.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <form action="/index" method="get">
        用户名：<input type="text" name="uname" id=""/>
        密 码：<input type="password" name=""pwd />
        <input type="submit" value="登 录"/>
    </form>
</body>
</html>
```



- 网络爬虫工程师
- 数据分析
- 人工智能
- Python Web方向



















