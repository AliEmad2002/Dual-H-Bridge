# Brief:
Based on the **NCE609 N&P Channel 40V 14A TO-252-4L SMD Mosfet Transistor** IC and **ULN2804 SMD IC SOP-18-300mil Darlington Transistor Array** as a low-cost gate driver, a low-cost, small-size dual H-bridge is fromed.

# Design screenshots on CAD-SW:
![image](https://github.com/AliEmad2002/Dual-Full-H-Bridge/assets/99054912/e43a8474-f97d-40ff-8e3d-c44d1ac7e664)

![image](https://github.com/AliEmad2002/Dual-Full-H-Bridge/assets/99054912/9e791314-31a1-41e3-9965-81f3f9a6413d)

![image](https://github.com/AliEmad2002/Dual-Full-H-Bridge/assets/99054912/1de870a8-e2a0-4426-b2b1-23fb97779cf0)

(All through-hole pads, and vias, are of large diameter - 2mm - to ease soldering, espicially that fabrication is done manually in the lab)

# Design scematic:
![image](https://github.com/AliEmad2002/Dual-Full-H-Bridge/assets/99054912/96cd2c4a-0d25-4a2b-b2f5-e57ec8dbe168)

# Effect of fly-back diodes:
When driving iductive loads, 

# Gate switching time (On oscilloscope)
* To achieve higher effeciency, gate switching time should be minimized as possible.
* When the MOSFET is at seay state and is on (closed circuit), it has a very low voltage drop accross it (almost zero), thus, the power losses on it would be almost zero.
* When the MOSFET is at seay state and is off (opened circuit), it has a very low current through it (almost zero), thus, the power losses on it would be almost zero, too.
* Problem of long switching time is that MOSFET in this time has both voltage accross it and current through it of magnitudes larger than zero, hence power losses on it would not be zero, decreasing effecincy of the circuit.
* This timing depends mainly on capaciance of MOSFET's gate and its pulling resistor, also switching time of the gate-driver.
* Assuming a maximum switcing frequency of 100kHz for the whole circuit, to achive 98% effecincy, maximum switching time should be 2uS.
* Referring to datasheets of the two used IC's (mentioned above), it was found that:
  - Minimum switching times of **ULN2804** are: 0.1uS to turn on, 0.2uS to turn off.
  - Minimum switching times of **NCE609** are: 25nS to turn on, 48nS to turn off.
  - Gate charge of **NCE609**: 24nC.
  - Input capacitance of **NCE609**: 1500pF.
  - Gate threshold voltage of **NCE609**: ±1.5V
* The only thing to do in order to maximize usage of this information, is to make the gate capacitance and gate pulling resistor charge and discharge within MOSFET's parameters.
* Assuming Vcc = 24V.
* Using the following formula, turn on time of 0.2uS is achived:
  - ![image](https://github.com/AliEmad2002/Dual-Full-H-Bridge/assets/99054912/1c506dad-8adf-4ae6-a2b3-641baf6625fd)

    (Reference: http://hyperphysics.phy-astr.gsu.edu/hbase/electric/capchg.html)

    ![image](https://github.com/AliEmad2002/Dual-Full-H-Bridge/assets/99054912/fcb8934b-c6eb-48cc-8d49-7d3d6413bf6b)

    ==> R_max = 1213Ω  ==> use gate pulling resistor of 1kΩ.

* Turn off time is limited by ICs, as while turning off, the gate is directly connected to ground.  

# Lab-made PCB:

# Demo test:
This test runs two 12V-2A motors. Controlled by a PID controller on stm32f103c8t6:
