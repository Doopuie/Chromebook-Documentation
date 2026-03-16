# **Notes**





* Sh1mmer only works with some 3110 models, so some 3110s may have a different key/signature compared to other 3110s; the 
    key could be the HWID.

    * The CRET-BKLL and CRET360-HXIQ sections of the HWID do not seem to be the reason why the sh1mmer does not work. In fact it 
        is pretty clear now that they just reference what model they are. **(CRET-BKLL = 3110, CRET360-BKLL = 3110 2in1)**

    * C7B-G3F-I4I-48V-A6M-A2C-A7E <- **This HWID worked with sh1mmer**. **Side Note** These numbers seem to be completely random on 
        each board but I am hoping that there is some correlation between the ones that do not accept sh1mmer and the ones that do.
    
    * C8B-I2D-I4I-Q98-45A-I4I <- **This HWID worked with sh1mmer**

    * C8B-C2E-G4G-R2I-X8M-A6C-A4R <- **This HWID does not work with sh1mmer**





# **Useful Commands**





##### Developer Console





* vpd = Vital Product Data

* vpd -d = delete
* vpd -s = means set
* vpd -l = means list





# **3110**





##### No Touch Issue





1. Check both sides of F6 for continuity.
   
2. If that does not work, Check voltage on C295 (capacitor directly to the left of U35) for 5V, this is 5V input to U35.
   
3. Then check for 5V on C5032 (directly above U35, directly below F6), this is output from U35. 
   
4. If there is input but no output, replace U35.





# **Reading Schematics and Boardviews**





##### Naming schemes





* When I say "switch" I mean it could be a MOSFET, load switch, power switch, or any sort of IC.

* PP = Power Plane, large traces of copper used for transporting large amounts of current; indicates a large power rail.

* PP1800 = Power Plane 1.8V **Side Note** 1800 is in millivolts.
* PP3300 = Power Plane 3.3V
* PP5000 = Power Plane 5.0V

* _R = rail on the resistor side, created after a switch.
    (PP5000_TOUCH_S0_R: meaning 5V resistor side rail that only powers the touchscreen when the device is completely turned on.)

* _SW = rail after a switch.





##### Sleep "S" states





* S2 and S3 are not often used in modern systems, so I chose not to include them here.

* S0 = Fully on
* S3 = Sleep; everything is powered down except for RAM where the systems last state is stored.
* S4 = Hibernate; saves contents from memory to non-volatile storage before shutting down completely.
* S5 = Soft Off; everything is off except for essential components needed to boot up the device.