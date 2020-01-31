#爬取B站每天的排行榜（生成的文件必须要用WPS打开，excal会乱码）
import requests #导入模块
from bs4 import BeautifulSoup
import csv

url = 'https://www.bilibili.com/ranking' #爬取地址
txt = requests.get(url).text  #爬取html
soup = BeautifulSoup(txt,'html.parser') #列表解析
list = soup.find_all('li',{'class' : "rank-item"}) #筛选所需要的排行榜信息
class Video():
    def __init__(self,rank,title,visit,up,up_id):        #爬取信息
        self.rank = rank
        self.title = title
        self.visit = visit
        self.up = up
        self.up_id = up_id
    def set_message(self):
        return [self.rank,self.title,self.visit,self.up,self.up_id]
def write():
    return ['排名','标题','播放量','UP','UID']  #写入函数
messages = []

for li in list:   #循环
    title = li.find('div',{'class' : "info"}).find('a').text #爬取视频标题
    visit = li.find('span',{'class' : "data-box"}).text #播放量
    up = li.find_all('span',{'class' : "data-box"})[2].text #UP主
    up_id = li.find_all('a')[2].get('href')[len('//space.bilibili.com/'):] #UID
    rank = li.find('div',{'class' : "num"}).text
    mess = Video(rank,title,visit,up,up_id)
    messages.append(mess)


file_name = 'Top.csv'      #写入文件数据
with open(file_name,'w',encoding='utf-8') as f: #encoding='utf-8'很重要，mac好像不需要（在windows下面，新文件的默认编码是gbk）
    pen = csv.writer(f)
    pen.writerow(write()) #这里注意不要用writerows（一次写入多行）不然会出BUG!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
    for mess in messages:
        pen.writerow(mess.set_message())

