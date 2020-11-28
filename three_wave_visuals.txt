import numpy as np
import matplotlib.pyplot as plt
from matplotlib.widgets import Slider, Button, RadioButtons, TextBox
from collections import defaultdict
fig, ax = plt.subplots()
plt.subplots_adjust(left=0.15, bottom=0.25)
plt.ylim(-3,3)
t = np.arange(0.0, .2, 0.0001)
a0 = 1
f0 = 55
delta_f = 1
s = a0 * np.sin( f0 * t)
l, = plt.plot(t, s, lw=2, alpha = .5)
m, = plt.plot(t, s, lw=2, alpha = .5)
n, = plt.plot(t, s, lw=2, alpha = .5)

p, = plt.plot(t, s,color= 'black', lw=3)

ax.margins(x=0)


axcolor = 'lightgoldenrodyellow'
axfreq1 = plt.axes([0.25, 0.15, 0.65, 0.03], facecolor=axcolor)
axfreq2 = plt.axes([0.25, 0.10, 0.65, 0.03], facecolor=axcolor)
axfreq3 = plt.axes([0.25, 0.05, 0.65, 0.03], facecolor=axcolor)




sfreq1 = Slider(axfreq1, '', 55, 110, valinit=f0, valstep=delta_f)
sfreq2 = Slider(axfreq2, '', 55, 110, valinit=f0, valstep=delta_f)
sfreq3 = Slider(axfreq3, '', 55, 110, valinit=f0, valstep=delta_f)

axbox1 = plt.axes([.17,.15,.04,.03])
t1 = TextBox(axbox1, 'Note 1  ', initial='' )
axbox2 = plt.axes([.17,.10,.04,.03])
t2 = TextBox(axbox2, 'Note 2  ', initial='')
axbox3 = plt.axes([.17,.05,.04,.03])
t3 = TextBox(axbox3, 'Note 3  ', initial='')



def update(val):

    freq1 = sfreq1.val
    freq2 = sfreq2.val
    freq3 = sfreq3.val

    l.set_ydata(np.sin(freq1*2*np.pi*t))
    m.set_ydata(np.sin(freq2*2*np.pi*t))
    n.set_ydata(np.sin(freq3*2*np.pi*t))

    sumryz = np.sin(freq2*2*np.pi*t) + np.sin(freq1*2*np.pi*t) + np.sin(freq3*2*np.pi*t)
    p.set_ydata(sumryz)
    caption = lettername(freq1,freq2,freq3)
    t1.set_val(str(caption[0]))
    t2.set_val(str(caption[1]))
    t3.set_val(str(caption[2]))


def lettername(freq1,freq2,freq3):
    note1value = ''
    note2value = ''
    note3value = ''
    for value in notes:
        for oct in value:
            ex = float(oct)
            exl = ex-1
            exh = ex+1
            if freq1 > exl and freq1 < exh:
                if ex in value:
                    arc = value
                    note1value = list(libnotes.keys())[list(libnotes.values()).index(arc)]

                elif ex not in value:
                    return



    for value in notes:
        for oct in value:
            ex = float(oct)
            exl = ex - 1
            exh = ex + 1
            if freq2 > exl and freq2 < exh:
                if ex in value:
                    arc = value
                    note2value = list(libnotes.keys())[list(libnotes.values()).index(arc)]
                    print(arc,note2value)

                elif ex not in value:
                    return


    for value in notes:
        for oct in value:
            ex = float(oct)
            exl = ex-1
            exh = ex+1
            if freq3 > exl and freq3 < exh:
                if ex in value:
                    arc = value
                    note3value = list(libnotes.keys())[list(libnotes.values()).index(arc)]

                elif ex not in value:
                    return
    return note1value, note2value, note3value




sfreq1.on_changed(update)
sfreq2.on_changed(update)
sfreq3.on_changed(update)


resetax = plt.axes([0.8, 0.05, 0.05, 0.04])
button = Button(resetax, 'Reset', color=axcolor, hovercolor='0.975')


def reset(event):
    sfreq1.reset()
    sfreq2.reset()

button.on_clicked(reset)

A =	[55,	110,	220,	440,	880]
As =	[58.27,	116.54,	233.08,	466.16,	932.32]
B =	[61.74,	123.48,	246.96,	493.92,	987.84]
C =	[65.41,	130.82,	261.64,	523.28,	1046.56]
Cs =	[69.3,	138.6,	277.2,	554.4,	1108.8],
D =	[73.42,	146.84,	293.68,	587.36,	1174.72]
Ds =	[77.78,	155.56,	311.12,	622.24,	1244.48]
E =	[82.41,	164.82,	329.64,	659.28,	1318.56]
F =	[87.31,	174.62,	349.24,	698.48,	1396.96]
Fs =	[92.5,	185,	370,	740,	1480]
G =	[98,	196,	392,	784,	1568]
Gs = [103.83,	207.66,	415.32,	830.64,	1661.28]

final = [A, As, B, C, Cs, D, Ds, E, F, Fs, G, Gs]


for let in final:
    for oct in let:
        one = oct

for let in final:
    for oct in let:
        two = oct


# Initialize plot with correct initial active value
final = ['A', 'A#', 'B', 'C', 'C#', 'D', 'D#', 'E', 'F', 'F#', 'G', 'G#']
notes = [[55,	110,	220,	440,	880],
 [58.27,	116.54,	233.08,	466.16,	932.32],
 [61.74,	123.48,	246.96,	493.92,	987.84],
[65.41,	130.82,	261.64,	523.28,	1046.56],
 [69.3,	138.6,	277.2,	554.4,	1108.8],
	[73.42,	146.84,	293.68,	587.36,	1174.72],
[77.78,	155.56,	311.12,	622.24,	1244.48],
	[82.41,	164.82,	329.64,	659.28,	1318.56],
[87.31,	174.62,	349.24,	698.48,	1396.96],
[92.5,	185,	370,	740,	1480],
	[98,	196,	392,	784,	1568],
 [103.83,	207.66,	415.32,	830.64,	1661.28]]

libnotes = dict(zip(final, notes))


plt.show()