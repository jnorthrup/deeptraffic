# deeptraffic

most of the deeptraffic solutions i see on github look like brute force and overfitting, using mostly defaults.  i have made a graduated configuration that makes it interesting to watch the behaviors emerge in minutes 

I have also been able to make a few observations and build a few functions to grow an existing trained net without starting over.  

ref variable
===
starting at about `ref=7` you can coerce almost any desired behavior out of the net in a matter of a minute or two. as you plataeu (quickly in the lower ranks) you keep bumping up the ref, and occasionaly revisting the cluehammer (ref 6 or 7) when the net goes belly up.

by ref 17 (iteratively) you'll be able to squeeze low-70's out of a modest network and decide how to grow the capacity when you bottom out 

[ref - example](https://github.com/jnorthrup/deeptraffic/blob/master/net%20(18).js#L2)

a captivating ~15 minutes after net (18).js widening surgery from ref= 8 thru 13
![image](https://user-images.githubusercontent.com/73514/39670464-fcea409a-512f-11e8-853d-5a4edbbb5688.png)

brain surgery in deeptraffic
===

if and when you think it's likely you need to increase the dimensionality capacity of the hidden layers, the bridge+bias functions can help you wire in a new extension layer to the prior of the same size, allowing for a replication of the filters and/or bias away from the regression hot-spot.  it is assumed you have a refactoring editor like intellij or webstorm to lift out variables and splice the function pairs. 

[example - brain surgery in deeptraffic](https://github.com/jnorthrup/deeptraffic/blob/master/net%20(18).js#L6993)

bias function(s)
====
  * bias(n):  create a field of 1's to teleport a neighboring bias 1 layer away (and change the evolution hotspot in the process)
    * [example - bias](https://github.com/jnorthrup/deeptraffic/blob/master/net%20(18).js#L6946)
  
  * widenBias

filter function(s)
===
 * bridge(n): create a diagonal matrix of 1's as a filter at layer x+1 from trained layer x 
   * [example - bridge](https://github.com/jnorthrup/deeptraffic/blob/master/net%20(18).js#L6956)
![image](https://user-images.githubusercontent.com/73514/39615013-09630958-4f9e-11e8-8bb8-9a1e92ae69ef.png)


* widen(newSize, filterSize, old): if you change the depth of input this function acts like the bridge function and makes an effort not to overwhelm (0.1) the trained nets -- they will recover if you downstep ref 
   * [example - widen](https://github.com/jnorthrup/deeptraffic/blob/master/net%20(18).js#L6968) 
  

 * widenTemporalWithZeros(oldfilters): create non-zero temporal window setting and insert this as you would a bridge.  this creates new temporal filters with 0 - much like bridge  -- brain damage is inevitable, but not initally visible.   i did not see coherent salvagability when the unmasking of new tempooral inputs surfaced.  regression kept recurring worse each time, expect to go back to ref=7 or reset.  should probably go with .1 instead of 0 fills 
 
 * splitTemporal(oldfilters): asa above.   this attempts to duplicate the original input filters as new temporal entries with 0 action outputs -- the brain appears to get slightly muddy, may regress hard but will eventually detune the temporal inputs to whatever minimal value they serve.  this may assist in integrating the agents. 
 
Layer Widening
===
 
 * widenLayer(newSize,firstLayer,nextLayer)
 
 * widenLayerRandom (newSize,firstLayer,nextLayer)

[example widenLayerRandom](https://github.com/jnorthrup/deeptraffic/blob/master/net%20(22).js#L14902)
 

tweak - 2 dimensions for 4 directions, instead of 5 dimensions 
===

one of the tricks which may or may not lend to growing the net ad-hoc more easily is to reduce the dimensions of control to 2 layers instead of 5 - and it seems to encourage the all-important braking in a traffic jam which has eluded nearly every other agonizing brute force attempt i've made to date.

[example - tweak ](https://github.com/jnorthrup/deeptraffic/blob/master/net%20(18).js#L79)
