In order get the cisco 7975 to work with Asterisk you need to install chan_sccp and create users under the sip driver type. You will also need to install the sccp_manager.

After a lot of playing whilst you can get it to work under pjsip some of the functions to do not work and it is prone to erroring – SCCP is the most stable route I have found so far.

Install guide


Extract the Cisco7975TFTPConfig.zip
Update the SEPMACADDRESS.cnf.xml to be SEPyourmacaddress.cnf.xml of using the mac address of the phone.

Update SEPyourmacaddress.cnf.xml with the details of your sip server

Upload files to your TFTP server and update the Cisco phone

Please note : if in settings of the phone type **#** to reset
To factory reset power on the phone and when you see the first light appear hold # and then when the lights start to flow type 123456789*0#

SSH onto your voip server and run the following.

Yum install git mc nano asterisk-devel

cd /usr/src/
git clone https://github.com/chan-sccp/chan-sccp.git
cd chan-sccp

./configure --enable-conference
make -j2
make install

vim /etc/asterisk/modules.conf
 noload => chan_skinny.so
 load => chan_sccp.so

cp sccp.conf.freepbx /etc/asterisk/sccp.conf
cp sccp_extensions.conf.freepbx /etc/asterisk/sccp_extensions.conf
cp sccp_hardware.conf.freepbx /etc/asterisk/sccp_hardware.conf

fwconsole restart

Once restarted in Asterisk under Admin – Module Admin upload and install the sccp_manager-14-2-0.11.zip 


![image](https://user-images.githubusercontent.com/39843876/176869617-4c6cedbb-d02b-4726-a504-f9ad8bb3b264.png)
