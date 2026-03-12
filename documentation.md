# **Notes**





* Some sh1mmers may have a different key/signature compared to some 3110 models. The key could be the HWID.
    * HWID: CRET-BKLL (3110) <- This worked with the sh1mmer.
    * HWID: CRET360-HXIQ (3110 2in1) <- This did not work with the sh1mmer.





# **Developer Console**





* vpd = Vital Product Data

* vpd -d = delete
* vpd -s = means set
* vpd -l = means list





# **3110**





##### Touch Issues





1. Check both sides of F6 for continuity.
   
2. If that does not work, Check voltage on C295 (capacitor directly to the left of U35) for 5V, this is 5V input to U35.
   
3. Then check for 5V on C5032 (directly above U35, directly below F6), this is output from U35. 
   
4. If there is input but no output, replace U35.





# **Reading Schematics and Boardviews**





##### Naming schemes





* When I say "switch" I mean it could be a MOSFET, load switch, power switch, or any sort of IC.

* _R = rail on the resistor side, created after a switch.
* _SW = rail after a switch.





##### Sleep "S" states





* S2 and S3 are not often used in modern systems, so I chose not to include them here.

* S0 = Fully on
* S3 = Sleep; everything is powered down except for RAM where the systems last state is stored.
* S4 = Hibernate; saves contents from memory to non-volatile storage before shutting down completely.
* S5 = Soft Off; everything is off except for essential components needed to boot up the device.