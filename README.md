`timescale 1ns / 1ps



module add4(S,Cy4,Cy_in,x,y);
input[3:0]x,y;
input Cy_in;
output [3:0]S;
output Cy4;
wire [2:0]Cy_out;
add B0(Cy_out[0],S[0],x[0],y[0],Cy_in);
add B1(Cy_out[1],S[1],x[1],y[1],Cy_out[0]);
add B2(Cy_out[2],S[2],x[2],y[2],Cy_out[1]);
add B3(Cy4,S[3],x[3],y[3],Cy_out[2]);
endmodule

module add(cy_out,sum,a,b,cy_in);
input a,b,cy_in;
output sum,cy_out;
sum s1(sum,a,b,cy_in);
carry c1(cy_out,a,b,cy_in);
endmodule

module sum(sum,a,b,cy_in);
input a,b,cy_in;
output sum;
wire t;
xor x1(t,a,b);
xor x2(sum,t,cy_in);
endmodule

module carry(cy_out,a,b,cy_in);
input a,b,cy_in;
output cy_out;
wire t1,t2,t3;
and g1(t1,a,b);
and g2(t2,b,c);
and g3(t3,c,a);
or g4(cy_out,t1,t2,t3);
endmodule
