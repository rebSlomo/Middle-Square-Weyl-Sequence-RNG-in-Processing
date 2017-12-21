# Middle-Square-Weyl-Sequence-RNG-in-Processing

The initial article: https://arxiv.org/pdf/1704.00358.pdf
Author: Bernard Widynski
Date: April 4, 2017

Background
To implemet an RNG in processing needs a minimal implementation of uint64 and related arihmetic.
For test and comparison - as given in the article - we use C code.

C code tested on https://www.tutorialspoint.com/compile_c_online.php

// Middle Square Weyl Sequence RNG
// written by Gabor Somogyi (rev 2017.12.20) based on
// https://arxiv.org/pdf/1704.00358.pdf
// Bernard Widynski - April 4, 2017

#include <stdio.h>
#include <inttypes.h>

uint64_t x = 0, w = 0, s = 0xb5ad4eceda1ce2a9;
inline static uint32_t msws() {
x *= x; x += (w += s); return x = (x>>32) | (x<<32);
}

int main()
{
  printf("MSWS Random Number Generator\n");
  printf("seed: %" PRIu64 "\n",s);
  printf("\n");
  for(int i=0; i<10; i++)
  {
    printf("%zu",msws());
    printf("\n");
  }
  return 0;
}

//----------------------

Runtime results:

$gcc -o main *.c
$main
MSWS Random Number Generator
seed: 13091206342165455529

3048033998
3746490460
411637087
3336355023
285663429
1194354350
927646759
568977855
1922357842
556645914

