# hass-utility_meter_alternative
an alternate approach to the official hass.io utility_meter

This code originally comes from 
https://github.com/home-assistant/home-assistant

full credit to @dgomes and @fabaff code.  I only added my bits.

The standard component is great, howver it did not suit my needs, and the devs did not think there was a need for change/enhancement.

I have put this up for those who would also need this approach.

So how is it different?

The standard component evaluates the "old_state" vs "state" of the source sensor.  Calculates the DIFF, and adds it to the current accumulated total (state). This is perfect, except if you have any "glitch" in data from the source sensor.  I got erratic accumulation in my environment, especially when restarting HASS.

This alternative component still has the original component's mode, but can be configured to use an alternative calculation mode, by setting "mode: alt": 

```
  pv_prod_meter_alt:
    source: sensor.pv_prod
    cycle: daily
    mode: alt
    tariffs:
      - normal   
```

The instead of attempting to calculate a delta on every change, this mode rather takes a "snapshot" of the sensor value on reset/initialization, and then simply subtracts it from the reported value from the source sensor.  IT makes it impervious to "glitches" in data.

It's not perfect though.  The downside is that if you have a sensor that resets to ZERO (0) randomly, this is not going to work for you.

Well There you go.
Enjoy.
