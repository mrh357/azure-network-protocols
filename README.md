<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create 2 Azure VMs (one running windows, one running ubuntu)
- Install wireshark on windows
- From the windows vm, ping the ubuntu vm perpetually
- Use the network security group to block the ping
- Filter by RDP, SSH, DNS, DHCP and observe traffic.
- When filtered with DHCP, request a new ip address to observe the traffic.

# observing network traffic with wireshark
#### [Made by Mat Harley with Scribe](https://scribehow.com/shared/observing_network_traffic_with_wireshark__Te0-rkWVSAequbghlOwTMg)


1\. Go to the azure portal and create 2 vms (1 running widows 10, and 1 running ubuntu). Create the windows VM first and make sure they are on the same network. For the ubuntu vm, when it asked about ssh authentication, I changed it from the keys to password)

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/f3bdc17c-f009-4b5c-a897-78c6b99dc828/screenshot.png?tl_px=125,0&br_px=1502,769&force_format=png&width=1120.0)


2\. Use RDP to remote into your windows VM. paste in the public IP address and log in.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/2b6825c0-a162-4fab-b631-96f6ea81573b/screenshot.png?tl_px=0,0&br_px=410,256&force_format=png&width=860)


3\. Go to <https://wireshark.org/download.html> and download wireshark.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/b62cfac9-12dc-4114-bf46-392eba37bcf3/screenshot.jpeg?tl_px=462,191&br_px=1322,672&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


4\. Follow the standard install, unless you need the other options.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/1c1b05d5-9986-4267-8e9a-7470d09fb92f/screenshot.jpeg?tl_px=969,622&br_px=1829,1103&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


5\. Open wireshark and click on the fin icon to start monitoring the network traffic.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/e779a4e7-89c8-404f-a672-e651bee793b4/screenshot.jpeg?tl_px=0,0&br_px=859,480&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=-12,28)


6\. Click on the search bar and type ICMP . If there is data in the chart, click the green fin to clear the chart.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/002c4351-2dbb-468f-a4ff-a52354dd3759/screenshot.jpeg?tl_px=0,0&br_px=1719,961&force_format=png&width=1120.0)


7\. Open the command prompt

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/33e5b011-7e43-4b5c-9dd0-d57770795ca1/screenshot.jpeg?tl_px=139,0&br_px=999,480&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,70)


8\. Type 'ping ipv4 -t' to ping the ubuntu PC

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/55692bf0-6e9a-49c7-a805-1412f3e41a7a/screenshot.jpeg?tl_px=0,0&br_px=1719,961&force_format=png&width=1120.0)


9\. Back in the Azure portal, navigate to your ubuntu vm and go to networking.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/7772430e-e014-4e9e-8d1d-2b3978391779/screenshot.jpeg?tl_px=0,219&br_px=859,700&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=63,212)


10\. Click "Add inbound port rule"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/d822a1fa-e91b-4438-b1d0-824b85442597/screenshot.jpeg?tl_px=1700,263&br_px=2560,744&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=640,212)


11\. Click "ICMP"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/9a74c473-ca86-4e1a-90da-5eaa585c51fe/screenshot.jpeg?tl_px=1596,370&br_px=2456,851&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


12\. Click "Deny"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/05b51d54-05d8-4949-aae2-869ca3b745b8/screenshot.jpeg?tl_px=1591,453&br_px=2451,934&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


13\. Click "Priority"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/d18bbff9-d222-4ecf-bbdf-2abe0e59ebbc/screenshot.jpeg?tl_px=1604,530&br_px=2464,1011&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


14\. Type "200" (the higher up in the order the earlier the rule will apply: ex 200 will be before 300)

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/ac2d8bbf-3534-421f-8b9a-08f9270bf46e/screenshot.jpeg?tl_px=840,290&br_px=2560,1251&force_format=png&width=1120.0)


15\. Click "Add"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/5a08cd2b-1279-4e3d-9123-a36bcdc6acf0/screenshot.jpeg?tl_px=1612,959&br_px=2472,1440&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,375)


16\. Go back to the RDP, and observe the request timeout as the security rule is applied

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/c1dea35b-e6cb-4327-abc8-10627fd09b2f/screenshot.jpeg?tl_px=230,374&br_px=1090,855&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


17\. Go back to the azure portal and click on the icmp rule.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/4551954d-8197-4f78-beb7-aab41db89e93/screenshot.jpeg?tl_px=1364,342&br_px=2224,823&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


18\. Click "Allow"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/f520b005-77b7-401b-82c6-0824b30f27b3/screenshot.jpeg?tl_px=1592,462&br_px=2452,943&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,212)


19\. Click "Save"

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/f347faed-eb64-4bcc-93ff-2f4690edda81/screenshot.jpeg?tl_px=1612,959&br_px=2472,1440&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,376)


20\. Go back to the RDP

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/76e425c2-f4f9-4e41-8b92-97fecb2686ec/screenshot.jpeg?tl_px=767,959&br_px=1627,1440&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=402,367)


21\. If the command prompt is frozen, press ctrl+c and it should resume

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/89baa30d-b963-4758-afb5-8169009c8932/screenshot.jpeg?tl_px=0,238&br_px=1719,1199&force_format=png&width=1120.0)


22\. Observe that the ping requests have resumed. when you are done, press ctrl+c to end the ping command.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/a6b2d3c3-0a79-476b-b7f7-38aaebfd336f/screenshot.jpeg?tl_px=0,0&br_px=1376,769&force_format=png&width=1120.0&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=189,25)


23\. Click on the search bar and type ssh (or tcp.port ==22) to filter traffic by ssh.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/8902d357-d3f4-4c13-acfd-7708f25043f1/screenshot.png?tl_px=0,0&br_px=859,480&force_format=png&width=860)


24\. Type 'ssh user@ipv4' (the username and ipaddress of the ubuntu vm.)

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/8cf15033-0360-4289-aa7c-87fbdfeb2d04/screenshot.jpeg?tl_px=0,244&br_px=1719,1205&force_format=png&width=1120.0)


25\. Type "yes" and hit enter

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/fe90bd52-2c23-4704-acc6-dbe44a05035e/screenshot.jpeg?tl_px=0,244&br_px=1719,1205&force_format=png&width=1120.0)


26\. Enter the password. observe the ssh traffic as you type in the command prompt.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/d55eb05e-7011-4025-ad7d-44106358f712/screenshot.jpeg?tl_px=0,244&br_px=1719,1205&force_format=png&width=1120.0)


27\. Type "exit" when you are done to exit ssh.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/f8d18690-7ea1-42c8-9b50-3a2ca0c26f27/screenshot.jpeg?tl_px=327,478&br_px=2046,1440&force_format=png&width=1120.0)


28\. Click on the search bar

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/2fbea19f-a2e8-4a2e-b5e6-08214e3f9403/screenshot.jpeg?tl_px=0,0&br_px=859,480&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=34,48)


29\. Type "dhcp" or "udp.port == 67 or 68" to filter by DHCP traffic. click on the green fin to clear the chart.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/7290858a-b2ae-4b9d-89d3-312caff49306/screenshot.jpeg?tl_px=0,0&br_px=1719,961&force_format=png&width=1120.0)


30\. Type "ipconfig /renew" hit enter and observe the dhcp traffic as the vm tries to get a new ip address.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/2a19d2ef-ac96-423e-b645-fe14d1ab59cd/screenshot.jpeg?tl_px=0,478&br_px=1719,1440&force_format=png&width=1120.0)


31\. Click on the search bar

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/c6aa1e72-c3eb-4508-b9b3-a79317b6ed2b/screenshot.jpeg?tl_px=0,0&br_px=859,480&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=85,54)


32\. Type "dns" or "tcp.port ==53" or "udp.port ==53" to filter by DNS traffic.

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/1bf80bf3-4982-41fe-90d0-5ccb5e756d2d/screenshot.jpeg?tl_px=0,0&br_px=1719,961&force_format=png&width=1120.0)


33\. Clear the chart

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/df8ff45d-e5ed-46a6-9e77-a5aa45349e4e/screenshot.jpeg?tl_px=0,0&br_px=859,480&force_format=png&width=860&wat_scale=76&wat=1&wat_opacity=0.7&wat_gravity=northwest&wat_url=https://colony-recorder.s3.us-west-1.amazonaws.com/images/watermarks/FB923C_standard.png&wat_pad=31,37)


34\. Type "nslookup [google.com](http://google.com)", hit enter, and observe the traffic as the vm returns ip addresses for google

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/36fb2ef8-1ae3-4ee3-8302-3a9ef67f89c5/screenshot.jpeg?tl_px=0,478&br_px=1719,1440&force_format=png&width=1120.0)


35\. Type "nslookup [disney.com](http://disney.com)", hit enter, and observe the traffic as the vm returns ipaddresses for disney.com

![](https://ajeuwbhvhr.cloudimg.io/colony-recorder.s3.amazonaws.com/files/2023-11-06/36c4bf66-aaf9-4aac-abcd-8b2326c05782/screenshot.jpeg?tl_px=0,478&br_px=1719,1440&force_format=png&width=1120.0)


36\. clean up your resource groups if you are done with them.


