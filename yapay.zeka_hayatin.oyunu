from tkinter import *
import tkinter
import random
from base64 import b16encode


class oyun:
    hücre_boyutu=15
    canvas_gen=1000
    canvas_yük=800
    kare_x=[]
    kare_y=[]
    oynati=False
    mouse_x=0
    mouse_y=0
    kareler_x=[[]]
    kareler_y=[[]]
    def __init__(self,master):
        self.kareler_x.clear()
        self.kareler_y.clear()
        asıl_canvas_gen=self.canvas_gen+int(self.canvas_gen/self.hücre_boyutu-1)
        asıl_canvas_yük=self.canvas_yük+int(self.canvas_yük/self.hücre_boyutu-1)
        
        window.geometry(str(int(asıl_canvas_gen))+"x"+str(int(asıl_canvas_yük)+50))
        
        kont=tkinter.Button(window,text="Tamam",command=lambda: self.ko())
        kont.pack(padx=0,pady=0,side=tkinter.RIGHT)
        durdur=tkinter.Button(window,text="Ştop",command=lambda: self.oynat(False))
        durdur.pack(side=tkinter.RIGHT)
        self.c=Canvas(window,bg="white",width=asıl_canvas_gen,height=asıl_canvas_yük)
        self.c.pack()
    
        for i in range(1,int(self.canvas_gen/self.hücre_boyutu),1):
            self.c.create_line((self.hücre_boyutu*i)+i,0,(self.hücre_boyutu*i)+i,asıl_canvas_yük,fill="black",width=1)
        
        for i in range(1,int(self.canvas_yük/self.hücre_boyutu),1):
            self.c.create_line(0,(self.hücre_boyutu*i)+i,asıl_canvas_gen,(self.hücre_boyutu*i)+i,fill="black",width=1)
        for i in range(0,int(self.canvas_gen/self.hücre_boyutu),1):
            self.kareler_x.append([])
            self.kareler_y.append([])
            for ii in range(0,int(self.canvas_yük/self.hücre_boyutu),1):
                self.kareler_x[i].append(0)
                self.kareler_y[i].append(0)
                
        self.c.bind('<Button-1>',self.dıkla_bilet_gomdere)
    def dıkla_bilet_gomdere(self,event):
        self.mouse_x=event.x
        self.mouse_y=event.y
        if(self.mouse_x<800 and self.mouse_x>0 and self.mouse_y>0 and self.mouse_y<600):
            x=int(self.mouse_x/(self.hücre_boyutu+1))*self.hücre_boyutu+int(self.mouse_x/(self.hücre_boyutu+1))
            y=int(self.mouse_y/(self.hücre_boyutu+1))*self.hücre_boyutu+int(self.mouse_y/(self.hücre_boyutu+1))
            if(self.kareler_x[int(self.mouse_x/(self.hücre_boyutu+1))][int(self.mouse_y/(self.hücre_boyutu+1))]==0):
                self.kareler_y[int(self.mouse_x/(self.hücre_boyutu+1))][int(self.mouse_y/(self.hücre_boyutu+1))]=1
                self.c.create_rectangle(x,y,x+self.hücre_boyutu+1,y+self.hücre_boyutu+1,fill="black")
            else:
                self.kareler_y[int(self.mouse_x/(self.hücre_boyutu+1))][int(self.mouse_y/(self.hücre_boyutu+1))]=0
                self.c.create_rectangle(x,y,x+self.hücre_boyutu+1,y+self.hücre_boyutu+1,fill="white")
            for a in range(0,self.kareler_x.__len__(),1):
                for c in range(0,self.kareler_x[a].__len__(),1):
                    self.kareler_x[a][c]=self.kareler_y[a][c]
        
    def oynat(self,durumu):
        self.oynati=durumu
    def rgb_color(self,rgb):
        return(b'#' + b16encode(bytes(rgb)))
    
    def ko(self):
        self.oynat(True)
        self.kontrol()
    
    def kontrol(self):
        for x in range(0,self.kareler_x.__len__(),1):
            for y in range(0,self.kareler_x[x].__len__(),1):
                komşu_sayısı=0
                for xk in range(-1,2,1):
                    for yk in range(-1,2,1):
                        if(not(xk==0 and yk==0) and not(x+xk<0 or y+yk<0) and not(x+xk>=self.kareler_x.__len__() or y+yk>=self.kareler_x[xk+x].__len__())):
                            komşu_sayısı+=self.kareler_x[x+xk][y+yk]
                xx=x*self.hücre_boyutu+x
                yy=y*self.hücre_boyutu+y
                if((komşu_sayısı<2 or komşu_sayısı>3) and self.kareler_x[x][y]==1):
                    self.kareler_y[x][y]=0
                    self.c.create_rectangle(xx,yy,xx+self.hücre_boyutu+1,yy+self.hücre_boyutu+1,fill="white")
                if(komşu_sayısı==3 and self.kareler_x[x][y]==0):
                    self.kareler_y[x][y]=1
                    self.c.create_rectangle(xx,yy,xx+self.hücre_boyutu+1,yy+self.hücre_boyutu+1,fill="black")
        for a in range(0,self.kareler_x.__len__(),1):
                for c in range(0,self.kareler_x[a].__len__(),1):
                    self.kareler_x[a][c]=self.kareler_y[a][c]
        if(self.oynati):
            self.c.after(100,lambda:self.kontrol())
    
window=Tk()
b=oyun(window)
window.mainloop()
