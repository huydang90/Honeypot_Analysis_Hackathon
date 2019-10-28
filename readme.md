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
    