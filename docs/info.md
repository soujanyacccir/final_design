<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

Explain how your project works
This design executes binary operations and outputs the result to the 7-segment display.
The instruction is made up of 8 total bits.

## How to test

Explain how to use your project
WORKING 

1.DP Switch.
  pin 1 ------- A2(MSB)
  pin 2 ------- A1
  pin 3 ------- A0(LSB)


  pin 4 ------- B2(MSB)
  pin 5 ------- B1
  pin 6 ------- B0(LSB)

  pin 7 ------- Control pin 1
  pin 8 ------- Control pin 2

# Operation 

>1.When control input(i.e pin 7 and 8 of dp switch) is 00 , Addition Operation is performed.
  Example: 
#          A2  A1  A0       B2  B1  B0       S3  S2  S1  S0
           1   0   1    +   1   0   1     =  1   0   1   0       (in decimal 5+5 = 10)

  



>2.When control input is 01 , Multiplication (designed using only mux) is performed.
  Example: 
#         A2  A1  A0       B2  B1  B0        P5 P4 P3 P2 P1 P0
          1   1   1    *    1   1   1        1  1  0  0  0  1     (in decimal 7*7=49)

Note: P5 is the most significant bit (MSB)
      P0 is the least significant bit (LSB) 



>3.When control input is 10 , Logical Opearation is performed.
  A2 A1 are considered as primary inputs.
  The remaining bits also act as inputs but they play prime role in selecting which opeartion to be performed.
  i.e AND , XOR , COMPARATOR Opeartion etc

  Example:
#        A0  B2  B1   B0                      Operation
         0   0   0    0                         LOGIC 0
         0   0   0    1                         AND 
         0   0   1    0                         A>B
         0   0   1    1                         A
         0   1   0    0                         A<B
         0   1   0    1                         B
         0   1   1    0                         XOR 
         0   1   1    1                         OR 
         1   0   0    0                         NOR 
         1   0   0    1                         XNOR 
         1   0   1    0                         B'
         1   0   1    1                         A + B' (random function)
         1   1   0    0                         A'
         1   1   0    1                         A'+ B' (random function)
         1   1   1    0                         NAND
         1   1   1    1                         LOGIC 1


>4. When control input is 11, ROM is used for doing Multiplication
  Here Two Roms is being utilized for operation . 
    First ROM works as  3:8 decoder 
  It  takes A2 A1 A0 as inputs and provides 8 memory location which is used to derive data lines D2 D1 D0.
   Below is the truth table showing the values, that is stores d2 d1 d0 values for entire  design.

   Example:
   1st ROM 
#       A2  A1   A0           D2   D1   D0     decimal    
        0   0    0            0    0    0         0            
        0   0    1            0    1    0         2 
        0   1    0            1    0    0         4 
        0   1    1            1    1    0         6 
        1   0    0            0    0    1         1 
        1   0    1            1    0    0         4 
        1   1    0            0    1    1         3 
        1   1    1            1    1    1         7.

    For 2nd Rom:
  It works as a 6:64 decoder .
  It takes 6 inputs D2,D1,D0 , B2,B1,BO and provides 64 memory location which is ultimately used to derive 6 
  output terms(ptoduct terms) 
  (msb)p5 p4 p3 p2 p1 p0(lsb).

  Example:
  2nd ROM
#       D2  D1  D0            B2   B1   B0       P5   P4   P3   P2   P1   P0    decimal 
        0   0   0             0    0    0        0    0    0    0    0    0        0 
                              0    0    1        0    0    0    0    0    0        0 
                              0    1    0        0    0    0    0    0    0        0 
                              0    1    1        0    0    0    0    0    0        0  
                              1    0    0        0    0    0    0    0    0        0 
                              1    0    1        0    0    0    0    0    0        0
                              1    1    0        0    0    0    0    0    0        0 
                              1    1    1        0    0    0    0    0    0        0

        0   1   0             0    0    0        0    0    0    0    0    0        0 
                              0    0    1        0    0    0    0    1    0        2 
                              0    1    0        0    0    0    1    0    0        4 
                              0    1    1        0    0    0    1    1    0        6 
                              1    0    0        0    0    1    0    0    0        8
                              1    0    1        0    0    1    0    1    0        12 
                              1    1    0        0    0    1    1    0    0        14 
                              1    1    1        0    0    1    1    1    0        16


                                   .
                                   .
                                   .
                                   .
                                   .
                                   .
                                   .
                                   .
                                   .
                                   

         1   1   1           0    0    0        0     0    0    0    0    0        0    
                             0    0    1        0     0    0    1    1    1        7 
                             0    1    0        0     0    1    1    0    0        14 
                             0    1    1        0     1    0    1    0    1        21 
                             1    0    0        0     1    1    1    0    0        28 
                             1    0    1        1     0    0    0    1    1        35 
                             1    1    0        1     0    1    0    1    0        42 
                             1    1    1        1     1    0    0    0    1        49



#  7 segment display .

   The a , b , c , d , f , g connections of all 4 blocks are ORed together.
   Thus the  final expressions of a b c d e f g are connected to the 7 seg.
   
   A clock is connected to dig1 pin of 7 seg and the same clock with an inverter is connecetd to the dig2 pin .


## External hardware

List external hardware used in your project (e.g. PMOD, LED display, etc), if any
no
