import schedule
from urllib.parse import unquote,quote
import time as tm, datetime
from schedule import every, repeat
import requests

list = [
    {'_token':"Nh4FL1QfegOo4iUdbdf9ICbv1OXW7tLT6SbMg6gT",'nid':"119920393571",'qid':"3278112","name":quote("عبدالحميد+عبدالسلام+السويح+القدافي)"),"resType":quote("تصوير+جديد")},
    # {'_token':"Nh4FL1QfegOo4iUdbdf9ICbv1OXW7tLT6SbMg6gT",'nid':"119960002033",'qid':"689977","name":quote("هشام+بن+شحنة"),"resType":quote("تصوير+جديد")},
    # {'_token':"Nh4FL1QfegOo4iUdbdf9ICbv1OXW7tLT6SbMg6gT",'nid':"119960002033",'qid':"689977","name":quote("هشام+بن+شحنة"),"resType":quote("تصوير+جديد")}
]


@repeat(every().sunday.at("10:00"))
def job():
    session = requests.Session()
    for registerer in list:
        while True:
            response = session.get(url="https://passrsrv.ly/")
            txtResponse = response.text
            if debuging == True:
                print(txtResponse)
                print(session.cookies.get_dict())
            if txtResponse.find("نأسف .. لقد إنتهت فترة الحجز") > 0:
                print(datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S"), " contineing...")
                session.close()
                continue
            else:
                postResponse = session.post(url="https://passrsrv.ly/save", data=registerer)
                postResponseText = postResponse.text
                if postResponseText.find("تم حفظ البيانات") > 0:
                    print(postResponseText)
                    break
                else:
                    print(datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S"), "\n",session.cookies.get_dict())
                    continue
                
debuging = False

while True:
    schedule.run_pending()
    tm.sleep(0.5)
    pass
