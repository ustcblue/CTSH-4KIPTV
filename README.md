将以下代码（来自 https://github.com/paulcx/Shanghai-Telecom-4k-iptv-with-merlin ）加入/koolshare/ss/rules/dnsmasq.postconf 

pc_append "dhcp-option-force=125,00:00:00:00:1a:02:06:48:47:57:2d:43:54:03:04:5a:58:48:4e:0a:02:20:00:0b:02:00:55:0d:02:00:2e      
dhcp-option=15
dhcp-option=28
dhcp-option=60,00:00:01:06:68:75:61:71:69:6E:02:0A:48:47:55:34:32:31:4E:20:76:33:03:0A:48:47:55:34:32:31:4E:20:76:33:04:10:32:30:30:2E:55:59:59:2E:30:2E:41:2E:30:2E:53:48:05:04:00:01:00:50" /tmp/etc/dnsmasq.conf
#robocfg vlan 51 ports "0t 1t 2t 3t 4t 8t" vlan 85 ports "0t 1t 2t 3t 4t 8t"
                                                     
vconfig set_name_type DEV_PLUS_VID_NO_PAD                                                                   
vconfig add eth0 85                          
vconfig add br0 85  
                                                    
brctl addbr vlan85                                                 
brctl addif vlan85 eth0.85                                                                                                                                                                                                                                                
brctl addif vlan85 br0.85                             
                                                                           
bcmmcastctl mode -i vlan85 -p 1 -m 1                     
bcmmcastctl mode -i vlan85 -p 2 -m 1
                                                                                            
ifconfig eth0.85 up                                          
ifconfig br0.85 up                
ifconfig vlan85 up          
                                                                      
vconfig add eth0 51                                  
brctl addif vlan85 eth0.51
ebtables -A FORWARD -i eth0.51 -o ! br0.85 -j DROP
ebtables -A FORWARD -o eth0.51 -j DROP
ifconfig eth0.51 up                         

# Shanghai-Telecom-4k-iptv-with-merlin

English Veriosn：

Shanghai Telecom 4K IPTV with Bridge Mode for Merlin

Please View http://koolshare.cn/thread-37102-1-1.html

中文版本：

上海电信4K IPTV桥接，仅限于梅林固件

使用方法请见http://koolshare.cn/thread-37102-1-1.html
