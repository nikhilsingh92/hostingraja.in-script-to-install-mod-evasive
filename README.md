# hostingraja.in-script-to-install-mod-evasive
The script explains how to install mod evasve in HostingRaja server


#!/usr/bin/env bash
ver_d=`rpm -qa \*-release | grep -Ei "oracle|redhat|centos" | cut -d"-" -f3`
httpd_conf_path="/etc/httpd/conf.d/";
mod_evas_file="mod_evasive.conf";
mod_evas_back="mod_evasive.conf_back";
null_file="/dev/null";
bcp_mod_file=$httpd_conf_path$mod_evas_back;
ocp_mod_file=$httpd_conf_path$mod_evas_file;
if yum list installed  |  grep -F 'mod_evasive' >>$null_file;
then 
	if [ -f $bcp_mod_file ]
	then 
		yes | cp -avr $bcp_mod_file $ocp_mod_file >>$null_file;
	fi	
else
	yum install mod_evasive -y  
fi

if [ $ver_d == "7" ]
then
	systemctl restart httpd >>$null_file ;

else
	service httpd restart >>$null_file ;
fi
#################################################################################################################

The mod_evasive Apache module, formerly known as mod_dosevasive, helps protect against DoS, DDoS (Distributed Denial of Service), and brute force attacks on the Apache web server. It can provide evasive action during attacks and report abuses via email and syslog facilities. The module works by creating an internal dynamic table of IP addresses and URIs as well as denying any single IP address from any of the following:

    Requesting the same page more than a few times per second
    Making more than 50 concurrent requests on the same child per second
    Making any requests while temporarily blacklisted

If any of the above conditions are met, a 403 response is sent and the IP address is logged. Optionally, an email notification can be sent to the server owner or a system command can be run to block the IP address. 

To install mod evasive you can run this shell script

If you need any more details about technical aspects kindly contact HostingRaja team or navigate to hostingraja.in
