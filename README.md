# Relay-Orbit-Determination
To find the ideal Orbit for a satellite to travel in around a body of radius, r, such that the communication is continuous on any point on that body with a signal strength of at least 80%

---

## Relay Orbit
To find the ideal Orbit for a satellite to travel in around a body of radius, r, such that the communication is continuous on any point on that body with a signal strength of at least 80%

<img width="1341" height="1239" alt="image" src="https://github.com/user-attachments/assets/750b64b2-5c0e-460e-8d27-67ea49e51e96" />

These 3 points are the vertices of an equilateral triangle. Therfore, if the radius is too small the vertices will pass throught the body and interrupt comms.

Too far out and communication to and from the body will lose strength.

Making the vertices a tangent to the circle would likely also cause problems as if the orbit changed slightly then the comms would be interrupted as the body intercepts the vertices.

Thus the altitude of the minimum allowable orbit would be r, the radius of the body. (see below)

<img width="1145" height="962" alt="image" src="https://github.com/user-attachments/assets/9f75a55e-5305-429f-8766-8ec51b0b1f4d" />

The upper bound would be the sphere of influence of the body (for now).

<img width="1218" height="1082" alt="image" src="https://github.com/user-attachments/assets/7d883db4-0bd3-472a-9f76-be43207911bc" />

As you can see above, the maximum distance from any satellite that isn't in the centre of the body is r, the radius of the orbit from the centre of the body, or 2 x radius of the radius of the body itself also.
From here on, the radius of the orbit from centre will be d, and radius of the body/orbit from surface will be r.

---

## Walkthrough

---

The first thing to know is the power range of each antenna.
For this example we will be using the HG-5 and Communotron 16

- HG5_power_km = 5000;
- Comm16_power_km = 500;

We then use these to calculate the range of comms between the two antenna.

- range = sqrt(HG5_power_km*Comm16_power_km);

Using the given signal strength formulae, signal = -2x^3 + 3x^2 and the fact that we want the signal strength to be at least 80%. We use this to calculate x.

- signal = 0.8;
- x = roots of, -2x^3 + 3x^2 - 0.8

We take the value where, 0 < x < 1, so that we get the correct distance.

- x = 0.71;

We then use the equation to calculate the distance, which is d in this case, the max distance between each satellite.

- distance = range*(1-x);

This gives an orbital distance above the surface of 258km.

We can also calculate the time period of the orbit.

- G = 6.67408e-11;
- M = 9.7599e20;
- T = sqrt((4 * pi^2 * (distance*1000)^3) / (G * M));
- T_hours = datestr(seconds(T),'HH:MM:SS');

---

## Evaluation

---
Ensure that the orbit isn't too close to the minimum, any deviation from the ideal orbit could lead to communication issues

<img width="741" height="886" alt="image" src="https://github.com/user-attachments/assets/f7140e2f-93cc-4cce-91e8-636787e1325c" />

As you can see here the distance of the orbit isn't much greater than the minimum
Ensure that the time period is large enough to be divisible by 3 and still a great enough difference from the normal time period to allow phasing the satellites into place
