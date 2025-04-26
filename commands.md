# COMMANDS
    index=* sourcetype="dhcp-logs"
    index=* sourcetype="dhcp-logs" | table src_ip, dst_ip
    
shows ip address that has the most count:
useful incase of analyzing bruteforce attack

     index=* sourcetype="dhcp-logs" | top limit=20 src_ip 
unique events

    index=* sourcetype="dhcp-logs" | table src_ip, dst_ip | dedup src_ip, dst_ip
