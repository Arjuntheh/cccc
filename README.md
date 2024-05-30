1. invr.v: 
module invr(x,y); 
input x; 
output y; 
wire vdd, gnd; 
assign vdd = 1'b1; 
assign gnd = 1'b0; 
pmos p1 (y,vdd,x); /* pmos name(drain, source, gate)*/ 
nmos n1 (y,gnd,x); /* nmos name(drain, source, gate)*/ 
endmodule 

invr_tb.v: 
module invr_tb; 
reg x1; 
wire y1; 
invr inv1 (x1,y1); 
initial begin 
x1 = 1'b0; #1 
x1 = 1'b1; #2 
$finish; 
end 
endmodule

2.buff.v: 
module buff(x,y); 
input x; 
output y; 
wire q,vdd, gnd; 
assign vdd = 1'b1; 
assign gnd = 1'b0; 
pmos p1 (q,vdd,x);
pmos p2 (y,vdd,q); 
nmos n1 (q,gnd,x); 
nmos n2 (y,gnd,q); 
endmodule 

buff_tb.v: 
module buff_tb; 
reg X1; 
wire Y1; 
buff buf1 (X1,Y1); 
initial begin 
X1=1'b0; #1 
X1=1'b1; #2 
$finish; 
end 
endmodule


3.nand.v: 
module nannd (x,y,z); 
input x,y; 
output z; 
wire q, vdd, gnd; 
assign vdd = 1'b1; 
assign gnd = 1'b0; 
pmos p1 (z,vdd,x); /* pmos name(drain, source, gate)*/ 
pmos p2 (z,vdd,y); 
nmos n1 (z,q,x); /* nmos name(drain, source, gate)*/ 
nmos n2 (q,gnd,y); 
endmodule 

module nannd_tb; 
reg x1, y1; 
wire z1; 
nannd nand1 (x1,y1,z1); 
initial begin 
x1 = 1'b0; y1 = 1'b0; #1 
x1 = 1'b0; y1 = 1'b1; #1 
x1 = 1'b1; y1 = 1'b0; #1 
x1 = 1'b1; y1 = 1'b1; #2 
$finish; 
end 
endmodule


4.and.v: 
module andmos (x,y,z); 
input x,y; 
output z; 
wire p, q, vdd, gnd; 
assign vdd = 1'b1; 
assign gnd = 1'b0; 
pmos p1 (q,vdd,x); /* pmos name(drain, source, gate)*/ 
pmos p2 (q,vdd,y); 
nmos n1 (q,p,x); /* nmos name(drain, source, gate)*/ 
nmos n2 (p,gnd,y); 
pmos p3 (z,vdd,q); 
nmos n3 (z,gnd,q); 
endmodule

and_tb.v: 
module andmos1; 
reg x1, y1; 
wire z1; 
andmos and1 (x1,y1,z1); 
initial begin 
x1 = 1'b0; y1 = 1'b0; #1 
x1 = 1'b0; y1 = 1'b1; #1 
x1 = 1'b1; y1 = 1'b0; #1 
x1 = 1'b1; y1 = 1'b1; #2 
$finish; 
end 
endmodule 


5.norr.v: 
module norr (x,y,z); 
input x,y; 
output z; 
wire q, vdd, gnd; 
assign vdd = 1'b1; 
assign gnd = 1'b0; 
pmos p1 (q,vdd,x); /* pmos name(drain, source, gate)*/ 
pmos p2 (z,q,y); 
nmos n1 (z,gnd,x); /* pmos name(drain, source, gate)*/ 
nmos n2 (z,gnd,y); 
endmodule

module norr_tb; 
reg x1, y1; 
wire z1; 
norr nor1 (x1,y1,z1); 
initial begin 
x1 = 1'b0; y1 = 1'b0; #1 
x1 = 1'b0; y1 = 1'b1; #1 
x1 = 1'b1; y1 = 1'b0; #1 
x1 = 1'b1; y1 = 1'b1; #2 
$finish; 
end 
endmodule 


6. orr.v: 
module orr (x,y,z); 
input x,y; 
output z; 
wire q, r, vdd, gnd; 
assign vdd = 1'b1; 
assign gnd = 1'b0; 
pmos p1 (q,vdd,x); /* pmos name(drain, source, gate)*/ 
pmos p2 (r,q,y); 
pmos p3 (z,vdd,r); 
nmos n1 (r,gnd,x); /* pmos name(drain, source, gate)*/ 
nmos n2 (r,gnd,y); 
nmos n3 (z,gnd,r); 
endmodule 

orr_tb.v: 
module orr_tb; 
reg x1, y1; 
wire z1; 
orr or1 (x1,y1,z1); 
initial begin 
x1 = 1'b0; y1 = 1'b0; #1 
x1 = 1'b0; y1 = 1'b1; #1 
x1 = 1'b1; y1 = 1'b0; #1 
x1 = 1'b1; y1 = 1'b1; #2 
$finish; 
end 
endmodule 


7. tgate.v: 
module tgate(a,s,y); 
input a,s; 
output y; 
pmos u1(y,a,~s); /* pmos name(drain, source, gate)*/ 
nmos u2(y,a,s); /* nmos name(drain, source, gate)*/ 
endmodule 

tgate_tb.v: 
module tgate_tb; 
reg in, sel; 
wire out; 
tgate u3(in,sel,out); 
initial begin 
in = 1'b0 ; sel = 1'b0 ; #10 
in = 1'b1 ; sel = 1'b0 ; #10 
in = 1'b0 ; sel = 1'b0 ; #10 
in = 1'b1 ; sel = 1'b0 ; #10 
in = 1'b0 ; sel = 1'b1 ; #10 
in = 1'b1 ; sel = 1'b1 ; #10 
in = 1'b0 ; sel = 1'b1 ; #10 
in = 1'b1 ; sel = 1'b1 ; #10 
$finish; 
end 
endmodule


8.  dff.v: 
module DFF(clk,rst,d,q,qb); 
input d,clk,rst; 
output q,qb; 
reg q; 
assign qb = ~q; 
always@ (posedge(clk)) 
begin 
if(rst) 
q <= 1'b0; 
else 
q <= d; 
end 
endmodule 

dff_tb.v: 
module DFF_tb; 
reg d,clk,rst; 
wire q,qb; 
DFF DFF1 (clk,rst,d,q,qb); 
initial begin 
clk = 1'b0; 
forever #1 clk = ~clk; 
end 
initial begin 
rst = 1'b1; d = 1'b0; #10 
rst = 1'b1; d = 1'b1; #10 
rst = 1'b1; d = 1'b0; #10 
rst = 1'b1; d = 1'b1; #10 
rst = 1'b0; d = 1'b0; #10 
rst = 1'b0; d = 1'b1; #10 
rst = 1'b0; d = 1'b0; #10 
rst = 1'b0; d = 1'b1; #10 
$finish; 
end 
endmodule 



9.jkff.v: 
module JKFF (clk,rst,j,k,q,qb); 
input j,k,clk,rst; 
output q,qb; 
reg q; 
assign qb = ~q; 
always @(posedge(clk)) 
begin 
if(rst) 
q <= 1'b0; 
else 
begin 
case ({j,k}) 
2'b00 : q <= q; 
2'b01 : q <= 1'b0; 
2'b10 : q <= 1'b1; 
2'b11 : q <= ~q; 
endcase 
end 
end 
endmodule

jkff_tb.v: 
module JKFF_tb; 
reg j,k,clk,rst; 
wire q,qb; 
JKFF jkff1(clk,rst,j,k,q,qb); 
initial begin 
clk = 1'b0; 
forever #1 clk = ~clk; 
end 
initial begin 
rst = 1'b1; j = 1'b0; k = 1'b0 ; #10 
rst = 1'b0; j = 1'b0; k = 1'b1 ; #10 
rst = 1'b0; j = 1'b1; k = 1'b0 ; #10 
rst = 1'b1; j = 1'b1; k = 1'b1 ; #10 
rst = 1'b0; j = 1'b0; k = 1'b0 ; #10 
rst = 1'b1; j = 1'b0; k = 1'b1 ; #10 
rst = 1'b1; j = 1'b1; k = 1'b0 ; #10 
rst = 1'b0; j = 1'b1; k = 1'b1 ; #10 
$finish; 
end 
endmodule 

10.  srf.v: 
module srff(clk,rst,s,r,q,qb); 
input s,r,clk,rst; 
output q,qb; 
reg q; 
assign qb = ~q; 
always @(posedge(clk)) 
begin 
if(rst) 
q <= 1'b0; 
else 
begin 
case ({s,r}) 
2'b00 : q <= q; 
2'b01 : q <= 1'b0; 
2'b10 : q <= 1'b1; 
2'b11 : q <= 1'bx; 
endcase 
end 
end 
endmodule 


srf_tb.v: 
module srff_tb; 
reg s,r,clk,rst; 
wire q,qb; 
srff u1(clk,rst,s,r,q,qb); 
initial begin 
clk = 1'b0; 
forever #1 clk = ~clk; 
end 
initial begin 
rst = 1'b1 ; s = 1'b0 ; r = 1'b0 ; #10 
rst = 1'b0 ; s = 1'b0 ; r = 1'b0 ; #10 
rst = 1'b0 ; s = 1'b0 ; r = 1'b1 ; #10 
rst = 1'b0 ; s = 1'b1 ; r = 1'b0 ; #10 
rst = 1'b0 ; s = 1'b1 ; r = 1'b1 ; #10 
rst = 1'b1 ; s = 1'b0 ; r = 1'b0 ; #10 
rst = 1'b1 ; s = 1'b0 ; r = 1'b0 ; #10 
rst = 1'b0 ; s = 1'b1 ; r = 1'b1 ; #10 
$finish; 
end 
endmodule 



11.  tff.v: 
module tff(clk,rst,t,q,qb); 
input t,clk,rst; 
output q,qb; 
reg q; 
assign qb = ~q; 
always @(posedge(clk)) 
begin 
if(rst) 
q <= 1'b0; 
else 
if(t) q <= ~q; 
end 
endmodule

tff_tb.v: 
module tff_tb; 
reg t,clk,rst; 
wire q,qb; 
tff u1 (clk, rst, t, q,qb); 
initial begin 
clk = 1'b0; 
forever #1 clk = ~clk; 
end 
initial begin 
rst = 1'b1; t=1'b0; #10 
rst = 1'b1; t=1'b1; #10 
rst = 1'b0; t=1'b0; #10 
rst = 1'b0; t=1'b1; #10 
rst = 1'b0; t=1'b0; #10 
rst = 1'b0; t=1'b1; #10 
$finish; 
end 
endmodule


12.  FAA.v: 
module FAA (a,b,ci,s,co); 
input a,b,ci; 
output s,co; 
wire vdd, gnd; 
assign vdd = 1'b1; 
assign gnd = 1'b0; 
assign s = a^b^ci; 
assign co = (a&b)|(b&ci)|(ci&a); 
endmodule

FAA_tb.v: 
module FAA_tb; 
reg a1,b1,ci1; 
wire s1,co1; 
FAA FA1 (a1,b1,ci1,s1,co1); 
initial begin 
a1=1'b0; b1=1'b0; ci1=1'b0; #2 
a1=1'b0; b1=1'b0; ci1=1'b1; #2 
a1=1'b0; b1=1'b1; ci1=1'b0; #2 
a1=1'b0; b1=1'b1; ci1=1'b1; #2 
a1=1'b1; b1=1'b0; ci1=1'b0; #2 
a1=1'b1; b1=1'b0; ci1=1'b1; #2 
a1=1'b1; b1=1'b1; ci1=1'b0; #2 
a1=1'b1; b1=1'b1; ci1=1'b1; #2 
$finish; 
end 
endmodule 

13.  padd.v: 
module padd (a,b,cin,s,cout); 
input [3:0]a,b; 
input cin; 
output [3:0]s; 
output cout; 
wire [3:1]c; 
FAA FA0 (a[0],b[0],cin,s[0],c[1]); 
FAA FA1 (a[1],b[1],c[1],s[1],c[2]); 
FAA FA2 (a[2],b[2],c[2],s[2],c[3]); 
FAA FA3 (a[3],b[3],c[3],s[3],cout); 
endmodule 
module FAA (a,b,ci,s,co); 
input a,b,ci; 
output s,co; 
wire vdd, gnd; 
assign vdd = 1'b1; 
assign gnd = 1'b0; 
assign s = a^b^ci; 
assign co = (a&b)|(b&ci)|(ci&a); 
endmodule 

padd_tb.v: 
module padd_tb;
reg [3:0]A,B; 
reg Cin; 
wire [3:0]S; 
wire Cout; 
padd PA1 (A,B,Cin,S,Cout); 
initial begin 
A=4'b0001; B=4'b0010; Cin=1'b1; #2 
A=4'b1111; B=4'b1111; Cin=1'b1; #2 
A=4'b1001; B=4'b1010; Cin=1'b1; #2 
A=4'b0001; B=4'b0010; Cin=1'b0; #2 
$finish; 
end 
endmodule 


14. sync_cntr.v: 
module syn_cntr (clk, rst, count); 
input clk, rst; 
output [3:0] count; 
reg [3:0] count; 
always @(posedge clk) 
begin 
if(!rst) /* considering active low reset */ 
count <= 4'b000;
else 
count <= count + 1; 
end 
endmodule 

sync_cntr_tb.v: 
module syn_cntr_tb; 
reg clk,rst; 
wire [3:0] count; 
syn_cntr u1 (clk, rst, count); 
initial begin 
clk = 1'b0; 
forever #1 clk = ~clk; 
end 
initial begin 
rst = 1'b0; #5 
rst = 1'b1; #40 
$finish; 
end 
endmodule 



15. async_cntr.v: 
module asyn_cntr (clk, rst, count); 
input clk, rst; 
output [3:0] count; 
wire high; 
assign high = 1'b1; 
jkff u1 (clk, rst, high, high, count[0]); 
jkff u2 (count[0], rst, high, high, count[1]); 
jkff u3 (count[1], rst, high, high, count[2]); 
jkff u4 (count[2], rst, high, high, count[3]); 
endmodule 
module jkff(clk, rst, j,k,q); 
input j,k,clk,rst; 
output q; 
reg q; 
always @(negedge clk or negedge rst) 
begin 
if (!rst) 
q <= 1'b0; 
else 
begin 
case ({j,k}) 
2'b00 : q <= q; 
2'b01 : q <= 1'b0; 
2'b10 : q <= 1'b1; 
2'b11 : q <= ~q; 
endcase 
end 
end 
endmodule 

async_cntr_tb.v: 
module asyn_cntr_tb; 
reg clk, rst; 
wire [3:0] count; 
asyn_cntr u1 (clk, rst, count); 
initial begin 
clk = 1'b0; 
forever #1 clk = ~clk; 
end 
initial begin 
rst = 1'b0; #5 
rst = 1'b1; #40 
$finish; 
end 
endmodul

16. carry_look_ahead.v:
module CarryLookAheadAdder(
input [3:0]A, B, 
input Cin,
output [3:0] S,
output Cout
);
wire [3:0] Ci; 

assign Ci[0] = Cin;
assign Ci[1] = (A[0] & B[0]) | ((A[0]^B[0]) & Ci[0]);
 
assign Ci[2] = (A[1] & B[1]) | ((A[1]^B[1]) & ((A[0] & B[0]) | ((A[0]^B[0]) & Ci[0])));
 
assign Ci[3] = (A[2] & B[2]) | ((A[2]^B[2]) & ((A[1] & B[1]) | ((A[1]^B[1]) & ((A[0] & B[0]) | ((A[0]^B[0]) & Ci[0])))));

assign Cout  = (A[3] & B[3]) | ((A[3]^B[3]) & ((A[2] & B[2]) | ((A[2]^B[2]) & ((A[1] & B[1]) | ((A[1]^B[1]) & ((A[0] & B[0]) | ((A[0]^B[0]) & Ci[0])))))));

assign S = A^B^Ci;
endmodule

module TB;
reg [3:0]A, B; 
reg Cin;
wire [3:0] S;
wire Cout;
wire[4:0] add;
CarryLookAheadAdder cla(A, B, Cin, S, Cout);
assign add = {Cout, S};
initial begin
$monitor("A = %b: B = %b, Cin = %b --> S = %b, Cout = %b, Addition = %0d", A, B, Cin, S, Cout, add);
A = 1; B = 0; Cin = 0; #3;
A = 2; B = 4; Cin = 1; #3;
A = 4'hb; B = 4'h6; Cin = 0; #3;
A = 5; B = 3; Cin = 1;
end
endmodule

