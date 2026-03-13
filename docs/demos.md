# Demos

## Fourier Transform Visualization

<h3>Wave Frequency Demo</h3>

Frequency 1  
<input type="range" id="f1" min="0" max="20" step="0.5" value="4">

Frequency 2  
<input type="range" id="f2" min="0" max="20" step="0.5" value="6">

Frequency 3  
<input type="range" id="f3" min="0" max="20" step="0.5" value="8">

<button py-click="update">Update Plot</button>

<div id="plot"></div>

<py-script>
import numpy as np
import matplotlib.pyplot as plt
from pyscript import Element

def create_wave(A, f, t):
    return A*np.sin(2*np.pi*f*t)

def update(event=None):

    f1 = float(Element("f1").value)
    f2 = float(Element("f2").value)
    f3 = float(Element("f3").value)

    N = 4000
    dt = 1/800

    t = np.arange(0,N)*dt

    y = create_wave(1,f1,t) + create_wave(1,f2,t) + create_wave(1,f3,t)

    fig, ax = plt.subplots()
    ax.plot(t,y)
    ax.set_xlim(0,2)
    ax.set_xlabel("Time")
    ax.set_ylabel("Amplitude")

    Element("plot").write(fig)

update()
</py-script>