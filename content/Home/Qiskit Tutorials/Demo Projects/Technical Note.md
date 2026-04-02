---
title: Drawing Circuits With Qiskit
---
#### On Linux Systems (Displaying Images)

In order to draw a circuit with qiskit, you must include, after creating the circuit 
```
qc.draw(output='mpl', filename='*.png')
```
where `*.png` is the desired filename of the circuit you want to create. On Mac, I believe (according to the YouTube tutorial series) that it is not necessary to include the `, filename='*.png'` part, and the rest will suffice. 

On my setup, the built-in terminal in nvim could not display these images, but executing the python file the same way (that is, `python *.py`) in the appropriate venv, in a *separate terminal* worked just fine. I used kitty terminal, and then, to open the image, I typed
```
xdg-open *.png
```
This is, in my opinion, preferable when you would like to use your created circuit figures somewhere (like I have for this blog). Tikz would work too in your LaTeX editor of choice, but it is obviously not specific to QC diagrams, and it is much more of a hassle in the long-run. 

#### Alternative Method (Text)

If, for whatever reason, the above method does not work out, it is much easier to display the output as text in a terminal. To do this, write instead of `qc.draw(output='mpl', filename='*.png')`:
```
print(qc.draw(output='text'))
```
The output will look something like:

![[public/Qiskit-Tutorials/Images/DemoCircuit-1a.png]]

*(This is a screenshot from my terminal, and it is the output of the demo circuit in the Qiskit documentation)*