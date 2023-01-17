# Analysis of Telekom Honeypot Data AI Hackathon

### Introduction

Deutsche Telekom operates a worldwide network of honeypots, computer systems that simulate weak points over the Internet, detect and report cyber attacks. Again and again the question arises, which interesting insights can be derived from the centrally collected data of the distributed sensors. Using machine learning / AI, the hackathon will analyze extracts of the honeypot data, for example to detect new attack patterns or to classify attacker groups. Ideally, it identifies high-quality attacks that stand out against the mass of widespread, automated attacks. The data are pre-qualified attack data recorded over a period of two weeks by the honeypots of DTAG and filed in a central ElasticSearch Index. Some data fields have been removed for privacy reasons. Each entry in the ElasticSearch index represents an attempted attack.

### Codebook:
    
    
    "vulnid"                      :   "CVE-ID of the attack classified, if available",
    "originalRequestString"       :   "Attack related information to be displayed on sicherheitstacho.eu, mostly URL of HTTP request (other data for other honeypot types)",
    "hostname"                    :   "Hostname of the honeypot, set by T-Pot 17.10 to random hostname during bootstrap",  
    "layers.ip.geoip_src_country" :   "Name of the country where they attacker is located"
    "layers.ip.geoip_dst_country" :   "Name of the country the honeypot is located"
    "layers.ip.location"          :   "Geolocation of the attacker"
    "layers.ip.dst_location"      :   "Geolocation of the target"
    "layers.ip.geoip_dst_asnum"   :   "Autonomous System (AS) of the external honeypot IP (might be private IP range)"
    "layers.ip.geoip_src_asnum"   :   "Autonomous System (AS) of the attacker" 
    "layers.ip.src"               :   "Source IP of the attacker"
    "layers.tcp.dstport"          :   "Destination port on the honeypot"
    "layers.tcp.srcport"          :   "Source port of the attacker"
    "targetEntryPort"             :   "Destination port on the honeypot",
    "sourceEntryPort" :           :   "Source port of the attacker",
    "rawhttp"                     :   "Raw http request headers in case the attack is delivered via an http request"
    "createTime"                  :   "Time of the attack (on the honeypot)"
    "receivedTime"                :   "Time of the attack transmission to backend(when the attack was received in the backend)"
    "additionalData"              :   "Optional additional data, e.g. md5 of corresponding payloads or binaries captured"
    
### Analysis:

Looking at the distribution of the attacks, it seems that the source of these attacks came mainly from Canada, the US, Russia and China. However, these are based on IP addresses which can be of the hosts that are affected by the hackers. Still, it gives us an interesting look at what countries are often chosen in the master-slave hierarchy. 

<p align="center">
  <img src="https://github.com/huydang90/Honeypot_Analysis_Hackathon/blob/master/Graphs/attack_by_countries.png"/>
</p>


The more interesting insight comes by analyzing the time-series data of all the attacks on the honeypots. The frequency of these attacks shows a clear pattern of autocorrelation. It seems that every 2 days, the behavior of attack repeat itself, in terms of intensity and time. This is an important discovery as this means that there is a possibility of forecasting the next waves of attacks, which means the system administrator can better reinforce the network for potential hacking attempts. Unstationary time-series are impossible to forecast but those that have embedded autocorrelation can be accurately predicted to a certain margin. 

<p align="center">
  <img src="https://github.com/huydang90/Honeypot_Analysis_Hackathon/blob/master/Graphs/overall_attack_time_series.png"/>
</p>


Looking further into the individual IP levels (of the top 20 bad IP addresses). It seems that there are 2 main patterns of attack: extreme regularity and extreme erraticity. 

We hypothesize that the regular patterns mimic the behavior of the affected servers that the attackers used, i.e an user that turns on their home computers after a day at work or office computers that are operated at regular intervals of time. 

<p align="center">
  <img src="https://github.com/huydang90/Honeypot_Analysis_Hackathon/blob/master/Graphs/top_IP_1.png"/>
</p>

<p align="center">
  <img src="https://github.com/huydang90/Honeypot_Analysis_Hackathon/blob/master/Graphs/top_IP_6.png"/>
</p>

### Solution Recommendation:

For the regular attacks, Recurrent Neural Networks with Long-short-term memory units can be utilized to effectively forecast the next waves of attacks. As seen in the following model, it’s able to pretty closely predict the volume of attacks that will happen next. With this knowledge, companies can prepare their defense for the attack ahead of time.

<p align="center">
  <img src="https://github.com/huydang90/Honeypot_Analysis_Hackathon/blob/master/Graphs/forecast_with_RNN.png"/>
</p>

For the irregular attacks, based on the database and libraries of known attacks, Generative Adversarial Neural Networks can be used to simulate new and unknown attacks that which can help to improve system defense as well. 



