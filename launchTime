# encoding:utf-8
# !/usr/bin/python
import csv
import time
import os

#app类 
class App(object):
    def __init__(self):
        self.content = ""
        self.startTime = 0
        
#启动App
    def LaunchApp(self):
        cmd = "adb shell am start -W -n com.tencent.mobileqq/com.tencent.mobileqq.activity.SplashActivity"
        self.content = os.popen(cmd)
    
#停止App
    def StopApp(self):
        cmd = "adb shell am force-stop com.tencent.mobileqq"
        #cmd = "adb shell input keyevent 3"
        os.popen(cmd)
#获取启动时间
    def GetLaunchTime(self):
        for line in self.content.readlines():
            if "ThisTime" in line:
                self.startTime = line.split(":")[1]
                break
        return self.startTime

#控制类
class Controller(object):
    def __init__(self,count):
        self.app = App()
        self.counter = count
        self.alldata = [("timestamp","elapsedtime")]
#单次测试过程
    def testprocess(self):
        self.app.LaunchApp()
        time.sleep(5)
        elapsedtime = self.app.GetLaunchTime()
        self.app.StopApp()          
        time.sleep(3)
        currenttime = self.getCurrentTime()
        self.alldata.append((currenttime,elapsedtime))
#多次执行测试过程
    def run(self):
        while self.counter > 0 :
            self.testprocess()
            self.counter = self.counter - 1
#获取当前时间戳
    def getCurrentTime(self):
        currentTime = time.strftime("%Y-%m-%d %H:%M:%S",time.localtime())
        return currentTime
#数据的存储
    def SaveDataToCSV(self):
#获取当前文件夹，也就是当前py文件所处的文件夹
        #current_path = os.getcwd()
#结合文件夹
        #path = current_path+"\\Users\Administrator\eclipse-workspace\appium-test\QQ\\"
        #csvfile = file(path+"twse_com_tw.zho_CHN.UTF8.csv", 'wb')
        
        csvfile = file("startTime_1.txt","wb")
        #获取文件操作句柄
        writer = csv.writer(csvfile)
        #写入多行用writerows
        writer.writerows(self.alldata)
        csvfile.close()
        
if __name__ == "__main__":
    controller = Controller(2)
    controller.run()
    controller.SaveDataToCSV()
