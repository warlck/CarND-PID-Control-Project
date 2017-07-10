# PID Controller

### Component Descriptions

* P component - P component in PID controller correspond to Proportional response. What it means is that magnitude of the conribution of P component is linear to input Cross Track Error (CTE) value. Depending on the coefficient Kp the P component will output steering signal in direction opposite to CTE. Since the value of P component is linearly related to CTE it is most sensitive CTE's magnitude. Hence if input to PID controller is large, unless we are careful, P component might output large steering angle, leading us to uncontrollable situation. Even if the required steering angle is large, we must be careful not make P compoment too sensitive to CTE, otherwise we will have very wobbly driving experience, or oversteering. 


* I component - Sometimes vehicles might have systematic bias. Example of such bias is misalignment of wheels of car by mechanic, or misalignment of wheels after vehicles go over road bump. Such bias will prevent vehicle from reaching our target of minimizing CTE and in steady state will lead to the vehicle driving in parallel to our target track. I component in PID controller correspond to Integral response. What it means is that magnitude of the contribution of I component will be determined by long term sum of the input CTE. Therefore, if we keep having large CTE inputs even if we steer in right direction, I component will detect this and add additional correction to steering angle, that will get us to target track. Since the I components takes into account all previous CTE inputs, the coefficient Ki must be small so that the integral component of PID output does not lead to huge steering values. Additionally, because our vehicle is moving from left to right of the target track, the CTE inputs will alternate in sign, preventing sum of CTEs from increasing infinitely (At least in our example project).


* D component - Even if the vehicle does not have any systematic bias, just relying on P component will cause the vehicle to constantly overshoot the target track and oscillate around it. D component of PID controller, which corresponds to Differential response, helps us to counter steer when we make progress in direction of target track. The magnitude of differential component depends on the rate of change of CTE with time.  If we make progress in direction of target track, the difference between current and previous CTE values will be negative, resulting in steering value opposite to P component's value. This counter steering helps us to smoothly reach the target track in the long term.



The sample video provided in output_video folder shows perfomance of project vehicle on the track with PID controller parameters set as follows: Kd = 0.2. Ki = 0.0004, Kd = 2.0;




### Tuning of the parametes

The parameters were tuned manually by simulating hill climbing algorithm. First I started with Kp set to 1.0 and rest to 0. After running the simulation, vehicle started to wobble pretty quickly. My intuition was to keep Kp component small for smooth steering, but apparently I had to keep it even smaller. Even adding setting Kd values  [1..5] did not change the violent steering. I set the values as follows: Kp = 0.1, Kd = 1.0, Ki = 0.0001.  The steering was much smoother and vehicle drove much further. However, at some sharp turns, the vehicle was not reacting fast enough. Increased Kp to 0.2 and most of the track the vehicle was crossing turns properly. There was one area where vehicle was getting off the road. So I tried increasing Kp to 0.3. The ride was mostly smooth, with little more jitter at some places, however the problematic area was still causing trouble. I have increased Kd to 5 and set Kp back to 0.2. Even though vehicle was successfully passing track without leaving the edges of the road, there was a jitter of constant steering angle correction. Descreasing Kd value to 3.0 smoothened those jitters, however not completely. Since there was not much systematic bias, the contribution of I component was very subtle. However after trying to increase Ki values by 0.0001 step until 0.0008 was reached, 0.0004 seemed to result in slightly more smoother ride. 

