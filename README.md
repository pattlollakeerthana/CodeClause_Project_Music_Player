import pygame
import tkinter
from tkinter import*
from tkinter.filedialog import askdirectory
import os

root=tkinter.Tk()
root.title("Music Player")
root.geometry('1200x1200')
root.configure(bg="#0f1a2b")

img=PhotoImage(file="Internship_Task-3_music-logo.png")
root.iconphoto(False,img)

heading=tkinter.StringVar()
heading.set("Select the song to play")

os.chdir(askdirectory())
songlist=os.listdir()

root_listbox=tkinter.Listbox(root,font="Helvetica 12 bold",width=120,height=30,bg="tan",fg="black",selectmode=tkinter.SINGLE)

for item in songlist:
    root_listbox.insert(0,item)

pygame.init()
pygame.mixer.init()

songstatus=StringVar()
songstatus.set("Choosing the song")

def playsong():
    pygame.mixer.load(root_listbox.get(tkinter.ACTIVE))
    name=root_listbox.get(tkinter.ACTIVE)
    heading.set(name)
    songstatus.set("Playing")
    pygame.mixer.music.play()

def pausesong():
    songstatus.set("Paused")
    pygame.mixer.music.pause()


def resumesong():
    songstatus.set("Resumed")
    pygame.mixer.music.unpause()

def stopsong():
    songstatus.set("Stopped")
    heading.set("Select the ong to play")
    pygame.mixer.music.stop()

def Nextsong():
    next_song=root_listbox.curselection
    next_song=next_song[0]+1
    temp=root_listbox.get(next_song)

    pygame.mixer.music.load(temp)
    pygame.mixer.music.play()

    heading.set(temp)
    songstatus.set("Playing")
    root_listbox.selection_clear(0,END)

    root_listbox.activate(next_song)

    root_listbox.selection_set(next_song)


def Previoussong():

    previous_song=root_listbox.curselection()
    previous_song=previous_song[0]-1
    temp2=root_listbox.get(previous_song)

    pygame.mixer.music.load(temp2)
    pygame.mixer.music.play()

    heading.set(temp2)
    songstatus.set("Playing")
    root_listbox.selection_clear(0,END)
    root_listbox.activate(previous_song)
    root_listbox.selection_set(previous_song)

    text=tkinter.Label(root,font="Helvetica",textvariable=heading).grid(row=0,columnspan=6)
    text1=tkinter.Label(root,font="Helvetica",textvariable=songstatus).grid(row=0,columnspan=6)

    root_listbox.grid(columnspace=6)

    play_btn=tkinter.Button(root,width=7,height=1,font="Helvetica",text="Play",command=playsong,bg="lightgreen").grid(row=3,column=0)
    

    pause_btn=tkinter.Button(root,width=7,height=1,font="Helvetica",text="Pause",command=pausesong,bg="lightblue",fg="black").grid(row=3,column=1)
    
        
    resume_btn=tkinter.Button(root,width=9,height=1,font="Helvetica",text="Resume",command=resumesong,bg="lightpink",fg="black").grid(row=3,column=2)
    
       
    stop_btn=tkinter.Button(root,width=11,height=1,font="Helvetica",text="Stop",command=stopsong,bg="lightgreen",fg="black").grid(row=3,column=3)
    
    nstop_btn=tkinter.Button(root,width=11,height=1,font="Helvetica",text="Next Stop",command=Nextsong,bg="mistyrose2",fg="black").grid(row=3,column=4)

    psong_btn=tkinter.Button(root,width=11,height=1,font="Helvetica",text="Previous Stop",command=Previoussong,bg="lightyellow",fg="black").grid(row=3,column=5)

    root.mainloop()
