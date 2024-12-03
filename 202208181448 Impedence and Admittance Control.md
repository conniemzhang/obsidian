tags = #Controls, #Method

Impedence Control
---
Impedance can be imagined as a spring-damper system between the point and the displaced point. it outputs an acceleration 
Activates on displacement from desired point.
Same compliance behavior whether or not you have a force. You need high stiffness and damping in order to track the trajectory behavior.

Spring is always connected to the desired force.

Admittance can also imagines as a 
Image you init two points in free space, but the motion control. If you have no force, then you can track the reference very 
Activates spring behavior on force contact, otherwise it's only motion control.
Decoupled, motion control.

Performance is different. 

IMPEDENCE
Assume static friction, so then you need a particular force to voercome the friction, then you cannot track the reference, 
Small force = small acceleration = small torque, then if you have static firction that small torque may never move. So you could have a constant error. Poor stability. 

NO inner loop, params that cause oscillations ion admittance may not cause them here, because it is faster and will reach the reference point. 

Delay is from communication. Talking to the robot, and the computation time.

Useful for human-robot interaction, for tasks that do not require so much accuracy. Like polishing. Compliant on all axis, but then motion controlled on just one.

$Test$


Admittance Control
---
ADMITTANCE.
Motion controller will be able to compensate for small errors.
Separates free and constrained motion.
If you increase params until you have oscialltions, bc motion controller is fast inner loop, then you have large delayed deviation from origin, so then it may be too fast and overshoot.
Motion Control tracks reference in free space.