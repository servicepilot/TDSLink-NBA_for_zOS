
# TDSLink - NBA for z/OS APIs

* Integration of NBA for z/OS with ServicePilot is supported natively.
* These integrations and APIs are only available with the commercial version of NBA for z/OS.



  
### Get Network conversations metrics

URL: `{nbaforzos_url}/api/nettrace`

Method: `GET`

This API allows you to get active network conversations with statistics. The output is in `CSV` format (`,` separator). This csv is updated every minute.

Sample response:

```
firsttime,lasttime,clientagent,serveragent,clientip,clientport,clientprocess,serverip,serverport,serverprocess,proto,isserverlocal,bytesin,bytesout,packetsin,packetsout,tcpdupack,tcpretransmit,tcpwindow,tcpstart,tcpstartinprivate,tcpstartinpublic,tcpstartoutprivate,tcpstartoutpublic,tcpend,tcpendin,tcpendout,tcprejected,tcpreset,tcphostrt,tcpnetwrt,tcphostnb,tcpnetwnb
2023-05-09T14:36:18.697972Z,2023-05-09T14:36:18.697972Z,adcd,adcd,192.168.9.1,161,tcpip,192.168.9.1,1036,,udp,0,0,71,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
2023-05-09T14:36:45.306299Z,2023-05-09T14:36:45.338496Z,,adcd,10.1.1.33,9234,,192.168.9.1,83,nba4zos,tcp,1,271,345,4,6,0,0,0,1,1,0,0,0,1,0,1,0,0,19,0,1,0
2023-05-09T14:37:07.700510Z,2023-05-09T14:37:10.701708Z,adcd,adcd,192.168.9.1,161,tcpip,192.168.9.1,1037,,udp,0,71,71,1,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
2023-05-09T14:36:23.702382Z,2023-05-09T14:37:10.341902Z,,adcd,192.168.8.1,12000,,192.168.9.1,12000,vtam,udp,1,160,480,1,3,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
2023-05-09T14:36:45.339658Z,2023-05-09T14:36:45.363041Z,,adcd,10.1.1.33,9235,,192.168.9.1,83,nba4zos,tcp,1,315,2271,5,7,0,0,0,1,1,0,0,0,1,0,1,0,0,16,5,1,1
2023-05-09T14:36:24.204239Z,2023-05-09T14:37:10.842366Z,,adcd,192.168.7.1,12000,,192.168.9.1,12000,vtam,udp,1,161,483,1,3,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
2023-05-09T14:36:24.206120Z,2023-05-09T14:37:10.844711Z,,adcd,192.168.5.1,12000,,192.168.9.1,12000,vtam,udp,1,161,483,1,3,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
2023-05-09T14:36:24.208031Z,2023-05-09T14:37:10.854016Z,,adcd,10.1.1.110,12000,,192.168.9.1,12000,vtam,udp,1,160,480,1,3,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
2023-05-09T14:36:26.849896Z,2023-05-09T14:36:57.850276Z,,adcd,192.168.9.9,,tcpip,192.168.9.1,,,icmp,1,376,188,2,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
2023-05-09T14:36:12.695893Z,2023-05-09T14:37:10.701909Z,adcd,adcd,192.168.9.1,,tcpip,192.168.9.1,,,icmp,1,168,56,3,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0
...
```


## Get z/OS Logs

URL: `{nbaforzos_url}/api/logs`

Method: `GET`

This API allows you to receive live zOS system logs on a permanent HTTP connection.

Sample response:

```
N        ADCD    202110411.03.29.67TSU00075P NBA4ZOSF
N        ADCD    202110411.03.29.68STC00076TLO010I PTDS      MAX/TRANS=0000002  MAX/TERM=0000002  EVE/SEC=0000003
N        ADCD    202110411.03.29.71STC00076TLO012I PTERMM   END OF TDSLINK
N        ADCD    202110411.03.29.79STC00076-                                              --TIMINGS (MINS.)--            -----PAGING COUNTS----
N        ADCD    202110411.03.29.79STC00076-STEPNAME PROCSTEP    RC   EXCP   CONN    TCB    SRB  CLOCK   SERV  WORKLOAD  PAGE  SWAP   VIO SWAPS
N        ADCD    202110411.03.29.80STC00076-         TDSLINK     00    445      0    .06    .02   36.4   279K  STARTED      0     0     0     0
N        ADCD    202110411.03.29.80STC00076IEF404I NBA4ZOSF - ENDED - TIME=11.03.29
```

## Get Local applications

URL: `{nbaforzos_url}/api/stats/lapp`

Method: `GET`

This API allows you to get statistics and information about local applications in InfluxDB format.

* Application information: `host`, `protocol`, `port`, ...
* Application volume statistics: `packets`, `bytes`, `bps`, `pps`, ...
* Application TCP activity: `tcpstart`, `tcprejected`, `tcpwindow`, `tcpdupack`, ...
* Application TCP response times: `tcphostrt`, `tcpnetwrt`

Sample response:

```csv
localapp,host="adcd",proto="tcp",serverport=22,program="sshd4" packetsin=0,packetsout=0,bytesin=0,bytesout=0,maxppsin=0,maxppsout=0,maxbpsin=0,maxbpsout=0,tcpstart=0,tcpend=0,tcprejected=0,tcphostrt=0,tcpnetwrt=0,tcpdupack=0,tcpretransmit=0,tcpwindow=0,tcpstartinprivate=0,tcpstartinpublic=0,tcpstartoutprivate=0,tcpstartoutpublic=0,tcpendin=0,tcpendout=0,tcpreset=0,conversations=0 1618398282000000000
localapp,host="adcd",proto="tcp",serverport=23,program="telnet" packetsin=629,packetsout=676,bytesin=31014,bytesout=472169,maxppsin=9,maxppsout=9,maxbpsin=3606,maxbpsout=67554,tcpstart=5,tcpend=2,tcprejected=0,tcphostrt=106,tcpnetwrt=8,tcpdupack=1,tcpretransmit=3,tcpwindow=0,tcpstartinprivate=5,tcpstartinpublic=0,tcpstartoutprivate=0,tcpstartoutpublic=0,tcpendin=0,tcpendout=2,tcpreset=0,conversations=2,bytesintopip="10.1.1.170",bytesouttopip="10.1.1.170" 1618398282000000000
localapp,host="adcd",proto="tcp",serverport=80,program="httpd1" packetsin=0,packetsout=0,bytesin=0,bytesout=0,maxppsin=0,maxppsout=0,maxbpsin=0,maxbpsout=0,tcpstart=0,tcpend=0,tcprejected=0,tcphostrt=0,tcpnetwrt=0,tcpdupack=0,tcpretransmit=0,tcpwindow=0,tcpstartinprivate=0,tcpstartinpublic=0,tcpstartoutprivate=0,tcpstartoutpublic=0,tcpendin=0,tcpendout=0,tcpreset=0,conversations=0 1618398282000000000
```

  
## Get Remote applications

URL: `{nbaforzos_url}/api/stats/rapp`

Method: `GET`

This API allows you to get statistics and information about remote applications in InfluxDB format.

* Application information: `host`, `protocol`, `port`, `ip`, ...
* Application volume statistics: `packets`, `bytes`, `bps`, `pps`, ...
* Application TCP activity: `tcpstart`, `tcprejected`, `tcpwindow`, `tcpdupack`, ...
* Application TCP response times: `tcphostrt`, `tcpnetwrt`

Sample response:

```
remoteapp,host="adcd",rem_prot="tcp",rem_port=21,rem_ip="10.1.1.33",rem_stack_name="tcpip",rem_agr_name="ftp\ control" rem_pkt_in=135,rem_pkt_out=123,rem_byt_in=10583,rem_byt_out=7846,rem_pps_in=5,rem_pps_out=5,rem_bps_in=3545,rem_bps_out=2626,rem_pkt_64_in=31,rem_pkt_128_in=104,rem_pkt_256_in=0,rem_pkt_512_in=0,rem_pkt_1024_in=0,rem_pkt_1025_in=0,rem_pkt_64_out=76,rem_pkt_128_out=47,rem_pkt_256_out=0,rem_pkt_512_out=0,rem_pkt_1024_out=0,rem_pkt_1025_out=0,rem_pkt_frag_in=0,rem_pkt_frag_out=0,rem_tcp_cn_sta=9,rem_tcp_cn_sto=10,rem_tcp_cn_rej=0,rem_tcp_cn_act=0,rem_max_hrt=280,rem_avg_hrt=11,rem_max_nrt=56,rem_avg_nrt=4,rem_tcp_dup_ack=0,rem_tcp_retrmt=0,rem_tcp_window=0,rem_hrt_inf_1=66,rem_hrt_inf_2=0,rem_hrt_inf_5=0,rem_hrt_inf_10=0,rem_hrt_sup_10=0,rem_nrt_inf_1=66,rem_nrt_inf_2=0,rem_nrt_inf_5=0,rem_nrt_inf_10=0,rem_nrt_sup_10=0,rem_frag_in_per=0.00,rem_frag_out_per=0.00,rem_dup_ack_per=0.00,rem_retrmt_per=0.00,rem_window_per=0.00 1618398393000000000
remoteapp,host="adcd",rem_prot="tcp",rem_port=25,rem_ip="10.1.1.33",rem_stack_name="tcpip",rem_agr_name="smtp" rem_pkt_in=5,rem_pkt_out=5,rem_byt_in=200,rem_byt_out=300,rem_pps_in=1,rem_pps_out=1,rem_bps_in=31,rem_bps_out=47,rem_pkt_64_in=5,rem_pkt_128_in=0,rem_pkt_256_in=0,rem_pkt_512_in=0,rem_pkt_1024_in=0,rem_pkt_1025_in=0,rem_pkt_64_out=5,rem_pkt_128_out=0,rem_pkt_256_out=0,rem_pkt_512_out=0,rem_pkt_1024_out=0,rem_pkt_1025_out=0,rem_pkt_frag_in=0,rem_pkt_frag_out=0,rem_tcp_cn_sta=0,rem_tcp_cn_sto=0,rem_tcp_cn_rej=5,rem_tcp_cn_act=0,rem_max_hrt=0,rem_avg_hrt=0,rem_max_nrt=0,rem_avg_nrt=0,rem_tcp_dup_ack=0,rem_tcp_retrmt=0,rem_tcp_window=0,rem_hrt_inf_1=0,rem_hrt_inf_2=0,rem_hrt_inf_5=0,rem_hrt_inf_10=0,rem_hrt_sup_10=0,rem_nrt_inf_1=0,rem_nrt_inf_2=0,rem_nrt_inf_5=0,rem_nrt_inf_10=0,rem_nrt_sup_10=0,rem_frag_in_per=0.00,rem_frag_out_per=0.00,rem_dup_ack_per=0.00,rem_retrmt_per=0.00,rem_window_per=0.00 1618398393000000000
```

  
## Get Interface metrics

URL: `{nbaforzos_url}/api/stats/intf`

Method: `GET`
  
This API allows you to get statistics and information about network interfaces in InfluxDB format.

* Interface information: `host`, `name`, `stack`, `ip`, ...
* Interface volume statistics: `packets`, `bytes`, `bps`, `pps`, ...
* Interface TCP activity: `tcpstart`, `tcprejected`, `tcpwindow`, `tcpdupack`, ...
* Interface TCP response times: `tcphostrt`, `tcpnetwrt`

Sample response:

```
interface,host="adcd",int_tcpip="tcpip",int_link_name="loopback",int_ip="127.0.0.1" int_pkt_in=6630,int_pkt_out=0,int_byt_in=421005,int_byt_out=0,int_pps_in=1,int_pps_out=0,int_bps_in=301,int_bps_out=0,int_pkt_64_in=3315,int_pkt_128_in=3315,int_pkt_256_in=0,int_pkt_512_in=0,int_pkt_1024_in=0,int_pkt_1025_in=0,int_pkt_64_out=0,int_pkt_128_out=0,int_pkt_256_out=0,int_pkt_512_out=0,int_pkt_1024_out=0,int_pkt_1025_out=0,int_pkt_frag_in=0,int_pkt_frag_out=0,int_tcp_cn_sta=0,int_tcp_cn_sto=0,int_tcp_cn_rej=0,int_tcp_cn_act=0,int_icmp_in=185640,int_icmp_out=0,int_igmp_in=0,int_igmp_out=0,int_tcp_in=0,int_tcp_out=0,int_igrp_in=0,int_igrp_out=0,int_udp_in=235365,int_udp_out=0,int_gre_in=0,int_gre_out=0,int_esp_in=0,int_esp_out=0,int_ah_in=0,int_ah_out=0,int_eigrp_in=0,int_eigrp_out=0,int_ospf_in=0,int_ospf_out=0,int_l2tp_in=0,int_l2tp_out=0,int_othr_in=0,int_othr_out=0,int_tcp_dup_ack=0,int_tcp_retrmt=0,int_tcp_window=0,int_load_in=0.00,int_load_out=0.00,int_frag_in_per=0.00,int_frag_out_per=0.00,int_dup_ack_per=0.00,int_retrmt_per=0.00,int_window_per=0.00,int_req_per_min=0,int_sta_in_priv=0,int_sta_in_pub=0,int_sta_out_priv=0,int_sta_out_pub=0,int_sto_in=0,int_sto_out=0,int_tcp_cn_res=0 1618398657000000000
interface,host="adcd",int_tcpip="tcpip",int_link_name="lnkvipa",int_ip="192.168.9.1" int_pkt_in=72179,int_pkt_out=178366,int_byt_in=4501888,int_byt_out=197101581,int_pps_in=426,int_pps_out=2147,int_bps_in=138011,int_bps_out=24109041,int_pkt_64_in=58223,int_pkt_128_in=4760,int_pkt_256_in=9010,int_pkt_512_in=86,int_pkt_1024_in=100,int_pkt_1025_in=0,int_pkt_64_out=19064,int_pkt_128_out=166,int_pkt_256_out=20212,int_pkt_512_out=11142,int_pkt_1024_out=1926,int_pkt_1025_out=125856,int_pkt_frag_in=0,int_pkt_frag_out=0,int_tcp_cn_sta=5626,int_tcp_cn_sto=5749,int_tcp_cn_rej=56,int_tcp_cn_act=5,int_icmp_in=1129907,int_icmp_out=319,int_igmp_in=0,int_igmp_out=0,int_tcp_in=3136616,int_tcp_out=193877940,int_igrp_in=0,int_igrp_out=0,int_udp_in=235365,int_udp_out=3223322,int_gre_in=0,int_gre_out=0,int_esp_in=0,int_esp_out=0,int_ah_in=0,int_ah_out=0,int_eigrp_in=0,int_eigrp_out=0,int_ospf_in=0,int_ospf_out=0,int_l2tp_in=0,int_l2tp_out=0,int_othr_in=0,int_othr_out=0,int_tcp_dup_ack=70,int_tcp_retrmt=1004,int_tcp_window=404,int_load_in=0.00,int_load_out=0.00,int_frag_in_per=0.00,int_frag_out_per=0.00,int_dup_ack_per=0.03,int_retrmt_per=0.40,int_window_per=0.16,int_req_per_min=0,int_sta_in_priv=5626,int_sta_in_pub=0,int_sta_out_priv=0,int_sta_out_pub=0,int_sto_in=40,int_sto_out=5584,int_tcp_cn_res=2 1618398657000000000
interface,host="adcd",int_tcpip="tcpip",int_link_name="samehlnk",int_ip="" int_pkt_in=0,int_pkt_out=0,int_byt_in=0,int_byt_out=0,int_pps_in=0,int_pps_out=0,int_bps_in=0,int_bps_out=0,int_pkt_64_in=0,int_pkt_128_in=0,int_pkt_256_in=0,int_pkt_512_in=0,int_pkt_1024_in=0,int_pkt_1025_in=0,int_pkt_64_out=0,int_pkt_128_out=0,int_pkt_256_out=0,int_pkt_512_out=0,int_pkt_1024_out=0,int_pkt_1025_out=0,int_pkt_frag_in=0,int_pkt_frag_out=0,int_tcp_cn_sta=0,int_tcp_cn_sto=0,int_tcp_cn_rej=0,int_tcp_cn_act=0,int_icmp_in=0,int_icmp_out=0,int_igmp_in=0,int_igmp_out=0,int_tcp_in=0,int_tcp_out=0,int_igrp_in=0,int_igrp_out=0,int_udp_in=0,int_udp_out=0,int_gre_in=0,int_gre_out=0,int_esp_in=0,int_esp_out=0,int_ah_in=0,int_ah_out=0,int_eigrp_in=0,int_eigrp_out=0,int_ospf_in=0,int_ospf_out=0,int_l2tp_in=0,int_l2tp_out=0,int_othr_in=0,int_othr_out=0,int_tcp_dup_ack=0,int_tcp_retrmt=0,int_tcp_window=0,int_load_in=0.00,int_load_out=0.00,int_frag_in_per=0.00,int_frag_out_per=0.00,int_dup_ack_per=0.00,int_retrmt_per=0.00,int_window_per=0.00,int_req_per_min=0,int_sta_in_priv=0,int_sta_in_pub=0,int_sta_out_priv=0,int_sta_out_pub=0,int_sto_in=0,int_sto_out=0,int_tcp_cn_res=0 1618398657000000000
```
  
## Get Network metrics

URL: `{nbaforzos_url}/api/stats/netw`

Method: `GET`

This API allows you to get statistics and information about networks in InfluxDB format.

* Network information: `host`, `subnetip`
* Network volume statistics: `packets`, `bytes`, `bps`, `pps`, ...
* Network TCP activity: `tcpstart`, `tcprejected`, `tcpwindow`, `tcpdupack`, ...
* Network TCP response times: `tcphostrt`, `tcpnetwrt`

Sample response:

```
network,host="adcd",net_ipaddr="10.1.1" net_pkt_in=71593,net_pkt_out=195138,net_byt_in=3577211,net_byt_out=242301404,net_pps_in=439,net_pps_out=2147,net_bps_in=141190,net_bps_out=24108786,net_pkt_64_in=65930,net_pkt_128_in=1544,net_pkt_256_in=3934,net_pkt_512_in=85,net_pkt_1024_in=100,net_pkt_1025_in=0,net_pkt_64_out=18955,net_pkt_128_out=213,net_pkt_256_out=5143,net_pkt_512_out=11117,net_pkt_1024_out=1935,net_pkt_1025_out=157775,net_pkt_frag_in=0,net_pkt_frag_out=0,net_tcp_cn_sta=5587,net_tcp_cn_sto=5711,net_tcp_cn_rej=61,net_tcp_cn_act=5,net_icmp_in=319,net_icmp_out=319,net_igmp_in=0,net_igmp_out=0,net_tcp_in=3576892,net_tcp_out=241499005,net_igrp_in=0,net_igrp_out=0,net_udp_in=0,net_udp_out=802080,net_gre_in=0,net_gre_out=0,net_esp_in=0,net_esp_out=0,net_ah_in=0,net_ah_out=0,net_eigrp_in=0,net_eigrp_out=0,net_ospf_in=0,net_ospf_out=0,net_l2tp_in=0,net_l2tp_out=0,net_othr_in=0,net_othr_out=0,net_max_hrt=5125,net_avg_hrt=61,net_max_nrt=69,net_avg_nrt=8,net_tcp_dup_ack=1414,net_tcp_retrmt=2957,net_tcp_window=404,net_hrt_inf_1=5840,net_hrt_inf_2=7,net_hrt_inf_5=5,net_hrt_inf_10=1,net_hrt_sup_10=0,net_nrt_inf_1=269,net_nrt_inf_2=0,net_nrt_inf_5=0,net_nrt_inf_10=0,net_nrt_sup_10=0,net_frag_in_per=0.00,net_frag_out_per=0.00,net_dup_ack_per=0.53,net_retrmt_per=1.11,net_window_per=0.15 1618398546000000000
network,host="adcd",net_ipaddr="192.168.5" net_pkt_in=0,net_pkt_out=5013,net_byt_in=0,net_byt_out=807093,net_pps_in=0,net_pps_out=1,net_bps_in=0,net_bps_out=127,net_pkt_64_in=0,net_pkt_128_in=0,net_pkt_256_in=0,net_pkt_512_in=0,net_pkt_1024_in=0,net_pkt_1025_in=0,net_pkt_64_out=0,net_pkt_128_out=0,net_pkt_256_out=5013,net_pkt_512_out=0,net_pkt_1024_out=0,net_pkt_1025_out=0,net_pkt_frag_in=0,net_pkt_frag_out=0,net_tcp_cn_sta=0,net_tcp_cn_sto=0,net_tcp_cn_rej=0,net_tcp_cn_act=0,net_icmp_in=0,net_icmp_out=0,net_igmp_in=0,net_igmp_out=0,net_tcp_in=0,net_tcp_out=0,net_igrp_in=0,net_igrp_out=0,net_udp_in=0,net_udp_out=807093,net_gre_in=0,net_gre_out=0,net_esp_in=0,net_esp_out=0,net_ah_in=0,net_ah_out=0,net_eigrp_in=0,net_eigrp_out=0,net_ospf_in=0,net_ospf_out=0,net_l2tp_in=0,net_l2tp_out=0,net_othr_in=0,net_othr_out=0,net_max_hrt=0,net_avg_hrt=0,net_max_nrt=0,net_avg_nrt=0,net_tcp_dup_ack=0,net_tcp_retrmt=0,net_tcp_window=0,net_hrt_inf_1=0,net_hrt_inf_2=0,net_hrt_inf_5=0,net_hrt_inf_10=0,net_hrt_sup_10=0,net_nrt_inf_1=0,net_nrt_inf_2=0,net_nrt_inf_5=0,net_nrt_inf_10=0,net_nrt_sup_10=0,net_frag_in_per=0.00,net_frag_out_per=0.00,net_dup_ack_per=0.00,net_retrmt_per=0.00,net_window_per=0.00 1618398546000000000
network,host="adcd",net_ipaddr="192.168.7" net_pkt_in=0,net_pkt_out=5014,net_byt_in=0,net_byt_out=807254,net_pps_in=0,net_pps_out=1,net_bps_in=0,net_bps_out=255,net_pkt_64_in=0,net_pkt_128_in=0,net_pkt_256_in=0,net_pkt_512_in=0,net_pkt_1024_in=0,net_pkt_1025_in=0,net_pkt_64_out=0,net_pkt_128_out=0,net_pkt_256_out=5014,net_pkt_512_out=0,net_pkt_1024_out=0,net_pkt_1025_out=0,net_pkt_frag_in=0,net_pkt_frag_out=0,net_tcp_cn_sta=0,net_tcp_cn_sto=0,net_tcp_cn_rej=0,net_tcp_cn_act=0,net_icmp_in=0,net_icmp_out=0,net_igmp_in=0,net_igmp_out=0,net_tcp_in=0,net_tcp_out=0,net_igrp_in=0,net_igrp_out=0,net_udp_in=0,net_udp_out=807254,net_gre_in=0,net_gre_out=0,net_esp_in=0,net_esp_out=0,net_ah_in=0,net_ah_out=0,net_eigrp_in=0,net_eigrp_out=0,net_ospf_in=0,net_ospf_out=0,net_l2tp_in=0,net_l2tp_out=0,net_othr_in=0,net_othr_out=0,net_max_hrt=0,net_avg_hrt=0,net_max_nrt=0,net_avg_nrt=0,net_tcp_dup_ack=0,net_tcp_retrmt=0,net_tcp_window=0,net_hrt_inf_1=0,net_hrt_inf_2=0,net_hrt_inf_5=0,net_hrt_inf_10=0,net_hrt_sup_10=0,net_nrt_inf_1=0,net_nrt_inf_2=0,net_nrt_inf_5=0,net_nrt_inf_10=0,net_nrt_sup_10=0,net_frag_in_per=0.00,net_frag_out_per=0.00,net_dup_ack_per=0.00,net_retrmt_per=0.00,net_window_per=0.00 1618398546000000000
```

## Copyright

© Copyright ServicePilot Inc 2023
