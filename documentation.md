# **Notes**




    
* Sh1mmer only works with some 3110 models, so some 3110s may have a different key/signature compared to other 3110s;

    * If the key/signature is the problem the HWID is not the key.

    * This is a copy of the debug info for a 3110 that the sh1mmer did not work on.
        
        HWID: CRET-BKLL C7B-G2I-J5J-S4R-W5E-A4A-A4I
        recovery_reason: 0x02 / 0x00 Recovery button pressed
        context.flags: 0x000000000030809c
        shared_data.status: 0x00000103
        nvdata: 60 10 00 00 00 02 00 4c 00 fe ff 00 00 ff ff 78
        dev_boot_usb: 0
        dev_boot_legacy: 0
        dev_default_boot: 0
        dev_boot_signed_only: 0
        TPM: fwver=0x00010001 kernver:0x00010004
        gbb.flags: 0x00000000
        gbb.rootkey: 941ff16caa37bdf3299955332c9e1b9cfdbed357
        gbb.recovery_key: 37018060a9234607239c05e99edfdce9f5ff5439
        read-only firmware id: Google_Cret.13606.573.0
        active firmware id: Google_Cret.13606.573.0
        battery level: 99%
        TPM state: v=1 failed tries=0 max_tries=200

    * This is a copy of the debug info for a 3110 that the sh1mmer did work on.

        HWID: CRET350-HXIQ C7B-B2D-H4H-48N-C6M-A2C-A2F
        recovery_reason: 0x00 / 0x00 Recovery not requested
        context.flags: 0x0000000000308088
        shared_data.flags: 0x00000142
        shared_data.status: 0x0000007e
        nvdata: 60 10 00 00 00 02 00 00 00 fe ff 00 00 ff ff 70
        dev_boot_usb: 0
        dev_boot_legacy: 0
        dev_default_boot: 0
        dev_boot_signed_only: 0
        TPM: fwver=0x00010001 kernver=0x00010004
        gbb.flags:0x00000000
        gbb.rootkey:941ff16caa37bdf3299955332c9e1b9cfdbed357
        gbb.recovery_key: 0839ba3e040eb2f8c9d3d19ee239b735f4c92851
        kernel_subkey: 230ab7861f739601eb1beffbef94b1f06a0506db
        read-only firmware id: Google_Cret.13606.426.0
        active firmware id: Google_Cret.13606.601.0
        battery level: 95%
        TPM state: v=1 failed tries=0 max_tries=200


        


# **Enrollment**





##### Removing Enrollment / Shimming





* You are not supposed to be able to remove enrollment by design unless you have access to school credentials. Which can then give
    you access to the schools google admin so you can decomission devices by service tag. Sh1mmer however, bypasses this somehow and removes the service tag from the device. I cannot say for certain, however, that it decomissions the device. 
    
    The Sh1mmer was made by the Mercury Workshop team, and they have website **https://sh1mmer.me/**, a github **https://github.com/MercuryWorkshop/sh1mmer**, as well as a discord server; which you can find on their website. 
    
    You would need a RAW RMA shim from Dell to make a sh1mmer. They used to have a website dedicated to providing RAW RMA shim files but they had to take it down for legal reasons. 

* Sometimes when a motherboard gets replaced and is assigned a new service tag (through a manual shim or sh1mmer), the old motherboard
    still retains that old service tag and acts like it is enrolled. The motherboard will not let you enter dev mode in this state and there are two ways you can get around this:

    **Only do this if the sh1mmer does not work**

    * Powerwash the device:

        1. Powerwash
        2. Go through the OOBE: Click Get Started, Choose a wifi.
        3. Enter Recovery Mode: Esc + Refresh + Power.
        4. Ctrl + D then Confirm to enter Developer Mode.
        5. Ctrl + D again to start the countdown into Developer Mode.
    
    * Clear Local Data:

        1. Enter recovery mode: Esc + Refresh + Power.
        2. Enter Developer Mode: Ctrl + D.
        3. Select return to Secure Mode. **Side Note** It should say "Confirm returning to Secure Mode" here, if it does, just do what it says.
        4. Once you return to Secure Mode, repeat steps one and two.
        5. Ctrl + D again to start the countdown into Developer Mode.





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