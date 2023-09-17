Unbricking a TP-Link router

Requirements:
- Firmware from the TP-Link website (must use the correct hardware version)
- A TFTP server which supports logging (this example uses TFTPD32/TFTPD64: https://tftpd32.jounin.net)
- Ethernet cable (preferably crossover cable)
- Computer or laptop
- The TP-Link router must be on the same LAN segment as your computer

Method:
Step 1) Download the firmware for your router from the TP-Link website, and then unzip the firmware file (.BIN file) into a suitable folder.

In this example, I have opened the ZIP file from the TP-Link website, extractred the .BIN file and placed it in the folder “C:\temp\”.
I am using a TP-Link AC1750 (Archer C7) router, hardware version is v2, and the firmware filename is “ArcherC7v2_en_eu_3_15_3_up_boot(180305).bin”.

![image](https://github.com/kadu247/archer_c20_v5_EU/assets/6238576/0afb87e9-791f-4079-ba85-b92d7bd31e5b)

Step 2) You must manually set the IP address of your computer/laptop according to the product you have:

Most TP-Link products:
Set the IPv4 address of the wired Ethernet interface on your computer to 192.168.0.66, and subnet mask to 255.255.255.0

TP-Link Pharos products:
Set the IPv4 address of the wired Ethernet interface on your computer to 192.168.0.100, and subnet mask to 255.255.255.0

Other TP-Link products:
Set the IPv4 address of the wired Ethernet interface on your computer to 192.168.0.225, and subnet mask to 255.255.255.0

![image](https://github.com/kadu247/archer_c20_v5_EU/assets/6238576/4f687aa4-8130-4eb5-9d06-3f0e9a71a8b9)

Step 3) Start the TFTP server, use the “Browse” button, and browse to the same folder from step #1, where the unzipped router firmware is (“C:\temp\”).

NOTE: You can either have the TFTP server listening on all interfaces by choosing “127.0.0.1”, or only on the specific Ethernet interface which we are using “192.168.0.66 or 192.168.0.100”.

![image](https://github.com/kadu247/archer_c20_v5_EU/assets/6238576/c8a171c8-9ea8-469b-94d9-4cb57b5556ae)

Step 4) Make sure that your computer has an Ethernet cable going to the TP-Link router.

NOTE: The router can actually be anywhere on the same LAN segment (plugged in to a switch or router), but since TFTP uses UDP as a transport protocol, the firmware file transfer will be more reliable if have the computer wired directly to the TP-Link router with an Ethernet cable.

Step 5) Ensure the TP-Link router is powered off. Hold down the reset button on the router and keep it depressed. Power the router on, wait for 5 seconds, and then release the reset button.

Step 6) Now, the router will now attempt to do a TFTP boot from your server at 192.168.0.66. You must use the TFTP server “log viewer” tab to see the filename which was requested by the router. When you have the filename, you will need to rename the firmware .BIN file to match what the router is requesting.

Each filename is specific to your model of TP-Link router, so ensure that you actually follow this process to determine the correct filename to use. Don’t use the filename in my example, otherwise it won’t work and you’ll be wasting time.

In this example, we can see that the router is requesting a file named “ArcherC7v2_tp_recovery.bin”.

Connection received from 192.168.0.86 on port 1957 [28/12 21:50:04.060]

Read request for file <ArcherC7v2_tp_recovery.bin>. Mode octet [28/12 21:50:04.060]

File <ArcherC7v2_tp_recovery.bin> : error 2 in system call CreateFile The system cannot find the file specified. [28/12 21:50:04.062]

![image](https://github.com/kadu247/archer_c20_v5_EU/assets/6238576/e54f2f58-f8da-42fe-9aaf-b65ee6e1c105)

Step 7) Now that we know which filename the router is looking for, we must rename our downloaded firmware file to whatever our router is requesting. This is how we effectively force the router to replace its current firmware.

In this example, the original filename of the firmware file which we downloaded from the official TP-Link website, is “ArcherC7v2_en_eu_3_15_3_up_boot(180305).bin”, but we will rename it to “ArcherC7v2_tp_recovery.bin”, as per the information we discovered in step #6.

![image](https://github.com/kadu247/archer_c20_v5_EU/assets/6238576/ae5c8348-fe70-451a-85e2-717d57109e06)

Step 8) Repeat step #5 of the process so that the router attempts another TFTP boot.

Step 9) Confirm in your TFTP server that the firmware was successfully downloaded by the router.

![image](https://github.com/kadu247/archer_c20_v5_EU/assets/6238576/22fdcaa5-6094-4ee2-9901-ea5b877ae5f7)

![image](https://github.com/kadu247/archer_c20_v5_EU/assets/6238576/91a13cc6-16b7-403a-99a9-2eac82c57a85)

Step 10) A few minutes after the firmware transfer, your router should install the new firmware. You can now set your computer/laptop network card to get an IP address via DHCP (which it will get from the router, if this process was successful) and you’ll be able to access the router’s web interface by using the factory-default settings:

- IP address: 192.168.0.1
- Username: admin
- Password: admin

![image](https://github.com/kadu247/archer_c20_v5_EU/assets/6238576/d8b990bb-bd6c-461f-8fd5-d3ba9189ef56)
