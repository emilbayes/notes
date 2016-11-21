# Generating Uniform Random Numbers
To generate random numbers from a uniform distribution $U(a, b)$, one might
attempt doing $(X mod d) + a, d = (b - a), X = U(0, N)$, however this assumes
that $N mod d \equiv 0$ which is only the case if $N|d$. One solution is to keepsampling $X$ until you get a number $\leq d$. This is acceptable if $d$ is close
to $N$. However if $d << N$ then instead of sampling a number in $[0, d]$, you
sample in a range divisible by $d$, which can be achieved by sampling in the
range $[0, N - (N mod d)]$ and then modulo this number to the desired range.

# Further questions

* It seems that $d > N/2 === d$ so the $[0, N - (N mod d)]$ only seems
  applicable for $d < N/2$

Sources:

http://stackoverflow.com/questions/10984974/why-do-people-say-there-is-modulo-bias-when-using-a-random-number-generator
http://eternallyconfuzzled.com/arts/jsw_art_rand.aspx
https://zuttobenkyou.wordpress.com/2012/10/18/generating-random-numbers-without-modulo-bias/

