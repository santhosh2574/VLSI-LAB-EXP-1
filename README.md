# SIMULATION OF LOGIC GATES ,ADDERS AND SUBTRACTORS

# AIM:
To simulate and synthesis Logic Gates,Adders and Subtractor using Vivado 2023.1.

# APPARATUS REQUIRED:
Vivado 2023.1.

# PROCEDURE:
1. Open Vivado: Launch Xilinx Vivado software on your computer.

2.Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3.Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4.Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5.Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6.Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7.Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8.Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9.View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

# Logic Diagram :
![330648335-f11c6378-915c-4d4b-8d9f-e5e4170c7887](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/37a27a62-a181-4aad-86f8-60f1a9d9a769)


# Half Adder:
![330648354-5fdd54ae-9bd2-40ed-9621-9aea405bdacc](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/96ef8b83-5404-4eb9-81a8-358abb70e665)



# Full adder:
![330648373-558a75f6-6e85-4f39-a6be-ddc5ea6c1bfb](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/91895aac-3171-4b01-b933-c05053aaf5d5)


# Half Subtractor:
![330648391-fe0560ff-5d15-48c6-9567-5da904536433](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/fe54cfb2-7c39-49ac-b5ed-262a762751eb)


# Full Subtractor:
![330648431-a04bd49e-555e-4308-9e2f-727291c533f9](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/822b5e32-0e77-4b0a-ae58-1bd8fc5ae419)



# 8 Bit Ripple Carry Adder
![330648444-566b63bb-d94a-4273-a9c6-d1c83e89f274](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/25e223ca-ed6f-45ed-889b-d818b31d8703)


# VERILOG CODE:
# Full Adder:
```
module fulladder (sum, cout, a,b,c);
input a,b,c;
output sum, cout;
wire w1,w2,w3,w4,w5;
xor x1(w1,a,b);
xor x2(sum,w1,c);
and al(w2,a,b);
and a2(w3,b,c);
and a3(w4,a,c);
or o1(w5,w2,w3); or o2(cout,w5,w4);
endmodule
```
# Full Subractor:
```
module full_subtractor(a, b, c,D, Bout);
input a, b, c;
output D, Bout;
assign D = a^b^c;
assign Bout = (a & b) | ((a^ b) & c);
endmodule
Half Adder:
module half_adder(a,b,sum,carry);
input a,b;
output sum,carry;
or(sum,a,b);
and(carry,a,b);
endmodule
```
# Half Adder:
```
module half_adder(a,b,sum,carry);
input a,b;
output sum,carry;
or(sum,a,b);
and(carry,a,b);
endmodule
```
# Half Subractor:
```
module half_subtractor(D,Bo,A,B);
input A,B;
output D,Bo;

assign D=A^B;
assign Bo=(~A)&B;
endmodule
```
# Logic Gates:
```
module logicgates(a,b,andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate);
input a,b;
output andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate;
and(andgate,a,b);
or(orgate,a,b);
xor(xorgate,a,b);
nand(nandgate,a,b);
nor(norgate,a,b);
xnor(xnorgate,a,b);
not(notgate,a);
endmodule
```
# Ripple Carry Adder 4Bit:
```
module rippe_adder(S, Cout, X, Y,Cin);
input [3:0] X, Y;// Two 4-bit inputs
input Cin;
output [3:0] S;
output Cout;
wire w1, w2, w3;fulladder u1(S[0], w1,X[0], Y[0], Cin);
fulladder u2(S[1], w2,X[1], Y[1], w1);
fulladder u3(S[2], w3,X[2], Y[2], w2);
fulladder u4(S[3], Cout,X[3], Y[3], w3);
endmodule
module fulladder(S, Co, X, Y, Ci);
input X, Y, Ci;
output S, Co;
wire w1,w2,w3;
xor G1(w1, X, Y);
xor G2(S, w1, Ci);
and G3(w2, w1, Ci);
and G4(w3, X, Y);
or G5(Co, w2, w3);
endmodule
```
# Ripple Carry Adder 8bit
```
module fulladder(a,b,c,sum,carry);
input a,b,c;
output sum,carry;
wire w1,w2,w3;
xor(w1,a,b);
xor(sum,w1,c);
and(w2,w1,c);
and(w3,a,b);
or(carry,w2,w3);
endmodule

module rca_8bit(a,b,cin,s,cout);
input [7:0]a,b;
input cin;
output [7:0]s;
output cout;
wire [7:1]w;
fulladder f1(a[0], b[0], cin, s[0], w[1]);
fulladder f2(a[1], b[1], w[1], s[1], w[2]);
fulladder f3(a[2], b[2], w[2], s[2], w[3]);
fulladder f4(a[3], b[3], w[3], s[3], w[4]);
fulladder f5(a[4], b[4], w[4], s[4], w[5]);
fulladder f6(a[5], b[5], w[5], s[5], w[6]);
fulladder f7(a[6], b[6], w[6], s[6], w[7]);
fulladder f8(a[7], b[7], w[7], s[7], cout);
endmodule
```
# OUTPUT:
# full adder
![330648496-c1712156-70cb-4a1f-b3e7-6beaef13327d](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/c12add9e-1216-499d-948c-95f0a1faed6c)


# Full Subractor
![330648543-dcddc3f6-af10-49a4-a6fc-451f526b05b8](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/898c7ab8-8d27-4a51-8a51-20af860655b1)


# Half Adder
![330648552-3e457a97-a0f1-4f6f-8357-f05647d78dca](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/ed1fab24-9f8e-4d04-81e7-c29c3708202e)


# Half Subractor
![330648624-dba5f8eb-7ceb-4603-8c2f-4a01fef4c0ac](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/12d2ef3b-5f03-48f8-93e2-41ee16e9b92e)


# Logic Gates
![330648637-56682163-e53b-4fc3-ba8c-6882d58adfac](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/a4574417-516f-4c50-8b06-46d4dc5bb87d)


# Ripple Carry Adder 4bit
![330648648-e15fff44-2e93-46e5-b529-42667257bc03](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/dbc21a88-eac0-43d7-9ee6-651039c896a0)


# Ripple Carry Adder 8bit
![330648660-9d846717-e7a7-482d-8264-bf662ae7c8f4](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/46ebefc3-76f7-496c-afcd-521f09ea5cc3)


# RTL Design:
# Full Adder
![330648746-f93e8601-b9af-4b82-bf62-f24a3b677bb1](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/a2eccfff-d2a5-4d64-892e-2dba6c8268f7)


# Full Subractor
![330648760-85b5752a-e00b-45c1-9100-88994039688a](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/5e978e62-9389-4749-834e-e4a11339dc1e)


# Half Adder
![330648769-3a9b91c1-cb5b-408d-9035-597e864f5305](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/02b771c7-9963-4be1-ad0a-0abee9684557)



# Half Subractor
![330648775-8db34254-22a4-4792-bd5f-b0951d9417b6](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/fe1953a5-a57f-401d-8876-7db9b8408b3b)



# Logic Gates
![330648789-91c33344-70fa-4c7c-aaa6-8d81a26bd8fd](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/984e86d7-ab42-4a98-b0a4-935dd94cc294)




# Ripple Carry Adder 4bit
![330648798-187c9ed1-7a07-46b8-ae34-c0d3d2b9de3a](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/4b69ad3f-8e7d-4725-9290-7fb3f8f77b1f)



# Ripple Carry Adder 8bit
![330648812-f347591d-f853-441c-b5c2-39537c2f7fed](https://github.com/santhosh2574/VLSI-LAB-EXP-1/assets/167754920/5b92e68a-deef-42ec-803a-40801f121f6c)



# Result:
Thus the simulate Logic Gates ,Adders and Subtractors is done and verified.
