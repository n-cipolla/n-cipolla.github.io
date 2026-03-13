# Demos

## Interactive Fourier Transform Visualization

Move the sliders to change the component frequencies.  
The left plot shows the time signal, the right shows the Fourier spectrum.

<div style="margin-bottom:20px">

Frequency 1
<input type="range" id="f1" min="0" max="20" step="0.5" value="4">

Frequency 2
<input type="range" id="f2" min="0" max="20" step="0.5" value="6">

Frequency 3
<input type="range" id="f3" min="0" max="20" step="0.5" value="8">

</div>

<div id="plot"></div>

<py-script>
import numpy as np
import matplotlib.pyplot as plt
from pyscript import Element

plt.rcParams["font.size"] = 12
plt.rcParams["font.family"] = "serif"

def create_wave(A,f,t):
    return A*np.sin(2*np.pi*f*t)

def update(event=None):

    f1=float(Element("f1").value)
    f2=float(Element("f2").value)
    f3=float(Element("f3").value)

    N=4000
    dt=1/800
    t=np.arange(0,N)*dt

    y1=create_wave(1,f1,t)
    y2=create_wave(1,f2,t)
    y3=create_wave(1,f3,t)

    y=y1+y2+y3

    freqs=np.fft.rfftfreq(N,dt)
    spectrum=np.abs(np.fft.rfft(y))

    fig,(ax1,ax2)=plt.subplots(1,2,figsize=(10,4))

    ax1.plot(t,y,color="black")
    ax1.set_xlim(0,2)
    ax1.set_xlabel("Time [s]")
    ax1.set_ylabel("Amplitude")
    ax1.set_title("Time Domain")

    ax2.plot(freqs,spectrum,color="black")
    ax2.set_xlim(0,25)
    ax2.set_xlabel("Frequency [Hz]")
    ax2.set_ylabel("Magnitude")
    ax2.set_title("Fourier Transform")

    fig.tight_layout()

    Element("plot").write(fig)

update()
</py-script>

<script>
document.querySelectorAll("#f1,#f2,#f3").forEach(el=>{
    el.addEventListener("input",()=>update())
})
</script>