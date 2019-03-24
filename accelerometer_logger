from microbit import *
import os

RANGE_2G = 0x00
RANGE_4G = 0x01
RANGE_8G = 0x02

ACCELEROMETER = 0x1D
CONTROL_REG1_STBY = [0x2a, 0x0]
CONTROL_REG1_ACT = [0x2a, 0x1]
XYZ_DATA_CFG = 0x0E
# SET_ACC_2G = [0x0E, 0x00]
# SET_ACC_4G = [0x0E, 0x01]
# SET_ACC_8G = [0x0E, 0x02]

def command(c):
    i2c.write(ACCELEROMETER, bytearray(c))

def set_acc_range(r=RANGE_4G):
    command(CONTROL_REG1_STBY)
    command([XYZ_DATA_CFG] + [r])
    command(CONTROL_REG1_ACT)
    
def read_file(filename):
    with open(filename) as f:
        line = f.readline()
        while line is not '':
            print(line, end='')
            line = f.readline()

def play_file(filename, de=20):
    with open(filename) as f:
        line = f.readline()
        while line is not '':
            print(line, end='')
            line = f.readline()
            sleep(de)

running = False
start_time = 0
counter = 0
data = []

file_prefix = "data"

# set sample rate, i.e. how many samples per second Hz
sample_rate = 10 # 50 times per second
period = 1000/sample_rate

dur = 5000

last_sent = 0

set_acc_range()

while True:
    if button_a.is_pressed() and running is False:
        sleep(250)
        running = True        
        counter = 0     
        display.show(Image.ANGRY, wait=False)
        start_time = running_time()
        
    
    if running is True and running_time() - start_time > dur:        
        end_time = running_time()
        running = False
        display.show(Image.HAPPY, wait=False)
        
        #now write the data out to a file
        count = len(os.listdir())
        #with open("data_{}.dat".format(count+1), mode='wt') as f:
        with open("data_{}.dat".format(count+1),'wt') as f:
            for d in data:
                f.write(str(d)+"\n")
        data = []
        
                
    if button_b.was_pressed() and running is False:
        files = os.listdir()
        for f in files:
            print("{f} - {s}".format(f=f,s=os.size(f)))
        
            
    if running:        
        if running_time() - last_sent > period:
            last_sent = running_time()
            data.append(accelerometer.get_values())
            counter = counter + 1
