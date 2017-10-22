## Reflection: ##

**Attribution:** I have completed this project with the help of Udacity's Project Overview Video on this project by David Silver and Sebastian's module on PID Control which is provided as classroom material. I would like to thank David, Sebastian and Udacity team for the insightful module and project review video which has enabled me to implement this project. 

**Disclaimer:** I initially thought of implementing twiddle method for Parameter tuning but I was not able to successfully implement the code for same and I was not able to get any help either so then I decided to watch the Project Overview Video by David Silver and I tuned the parameter using trial and error method.

**Iteration 1:**

Started with `kp = -1.0` while keeping Ki and Kd as 0.
Result: The car started nicely and started steering as well when it needed to. But then, the steering angle value was oscillating so much, it had no control over it. This was the situation of overshooting or say overcompensating the error since the feedback loop has only propertional term to correct the error. Eventually car got stuck at one point.

**Iteration 2:**

Reduced Proportional term to `-0.5` and added derivative term as `-0.5`, as suggested by David in the video. Idea of adding Derivative term is to minimize the amount of change. The derivative terms prevent drastic changes in the value and it impedes the rate of change.

Result: It started nicely and was able to continue better this time. But this time also car eventually got haywire and started steering madly, which is not the expected behaviour.

**Iteration 3:**

For rapid tuning of Kp, Ki and Kd cooefficients, we pass cooefficient values as argument to main() function instead of changing them in main.cpp everytime and recompiling the code. From this point onwards, I started passing values as argument instead of hardcoding it into the main.cpp file.

`kp:-0.25 ki:0 kd:-0.75:` The car was able to reach to the bridge this time and I was optimistic that even though with oscillations, it would complete the track. However, it got rotated to 180 degree angle on bridge and all of a sudden it just stopped moving.

**Iteration 4:**

`-0.25 0.001 -1.0:` The car was able to complete the lap using this setting, however this is still not the best setting because car oscillates on the bridge where the path is completely straight and the steering should be set straight to 0 degree angle their instead of oscillatory turns.

**Iteration 5:**

`-0.25 0 -1.0:` In this iteration, I just set Ki to 0, rest of the cooefficients were same as previous iteration (Iteration 4), and I don't see any major difference due to presence or absence of Ki = 0.001 in Iteration 4 and 5.

**Iteration 6:**

`-0.25 -0.01 -1.0:` Changed Ki to -0.01. This lead to even higher osciallations and car was not even able to reach till bridge. I believe this happened because value of cummulative error increased now due to higher value of Ki which in turn added more corrective action to the system.

**Iteration 7:**

`-0.25 -0.0001 -1.0:` The result of this setting was similar to Iteration 4, with the improvement in driving speed. So now I will tweak value of Kd for next iteration to see if I can reduce the oscillations.

**Iteration 8:**

`-0.25 -0.0001 -2.0:` This setting reduced the oscillations on the bridge as per my assumption, however, the car still oscillated near the end of lap. Speed however was also improved in this setting. Next iteration, I would try to reduce Kp value so that steering value can be reduced overall. It may also lead to higher speed possibly.

**Iteration 9:**

`-0.15 -0.0001 -2.0:` This setting worked amazingly and the car was able to drive successfully throughout the lap without leaving the track and without any heavy oscillations. Speed achieved in this setting is still 34 mph which I would like to improve so I will increase Kd value and will reduce Kp and Ki even further as a try.

**Iteration 10:**

`-0.10 -0.00001 -3.0:` The oscillations got improved further in this setting however car was almost on the edge of leaving track and top speed achieved was 32 mph in this setting. I will increase Ki value again to compensate better for system bias, while keeping Kp and Kd same in next iteration.

**Iteration 11:**

`-0.10 -0.0001 -3.0:` There is an improvement from previous iteration however still the top speed is 33 mph and there are instances when the car touches edge of the lane. Will increase Kp in the next iteration so that car can steer more in order to stay in the middle of lane while on steep curves. Will also increase kd to compensate for oscillations and drastic turns.

**Iteration 12:** 

`-0.20 -0.0001 -4.0:` This setting looks promising in terms of driving in the middle of lane as well as in terms of steering osciallations. However the speed is still 33 mph and I am not able to achieve more than that. Increasing Kp in next Iteration

**Iteration 13:**

`-0.40 -0.0001 -4.0:` Oscillations has increased in this setting. Increasing Kd in the next iteration to see if osciallations can be reduced with this Kp.

**Iteration 14:**

`-0.40 -0.0001 -6.0:` Unfortunately, the osciallations are not getting reduced even after increasing Kd. 

This is the expected result in terms of PID controller. There is a trade-off between the gains Kp, Ki and Kd but it doesn't mean that no matter what value we take for Kp, it can get compensated by Kd and Ki. Kp is a gain which gets multiplied by the error before feeding the error into correction loop. The higher the value of Kp, the higher value of error will be fed back which means the more corrective action will happen in the loop. 

As a result, even though when we try to impede rate of change to some value using Kd, still the overall change is big due to higher value of Kp. 

Ki on the other hand compensate for overall cummulative error introduced to the system, it keep tracks of history of the error too. It can compensate well for system bias, but it can't really compensate for higher value of Kp either. Instead, error introduced by Intergal controller also gets larger and larger over the time when we pick higher value of Kp. 

In my final iteration, I will be using the best working setting of Kp, Ki and Kd which I acheived in Iteration 12.

**Final Iteration:**

`kp:-0.20 ki:-0.0001 kd-4.0:` This setting gave me the top speed of 33 mph with least oscillations and without the car leaving the track. I am hardcoding this value in the main.cpp so that the code can be executed without passing command line arguments.