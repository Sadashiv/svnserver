yum update -y<br/>
yum update && yum install mod_dav_svn subversion httpd -y<br/>
vim /etc/httpd/conf.modules.d/10-subversion.conf<br/>
mkdir /opt/svn<br/>
htpasswd -cB /etc/httpd/subversion-auth svn<br/>
chgrp apache /etc/httpd/subversion-auth<br/>
chmod 660 /etc/httpd/subversion-auth<br/>
firewall-cmd --add-service=http --permanent<br/>
firewall-cmd --reload <br/>
svnadmin create /opt/svn/trunk<br/>
chown -R apache:apache /opt/svn/trun<br/>
chcon -R -t httpd_sys_content_t  /opt/svn/trunk<br/>
chown -R apache:apache /opt/svn/trunk<br/>
chcon -R -t httpd_sys_content_t  /opt/svn/trunk<br/>
vim /etc/sysconfig/selinux -Try with SELLINUX dsiabled if not make enable of SELINUX<br/>
Optional step-> chcon -R -t httpd_sys_content_t  /opt/svn/trunk<br/>
Optional step-> chcon -R -t httpd_sys_rw_content_t /opt/svn/trunk<br/>
systemctl restart httpd<br/>
<br/>
Open Browser<br/>
http://ip:80/svn/trunk<br/>
<br/>
Start wrking on the in your local<br/>
svn co http://ip:80/svn/trunk<br/>
cd trunk<br/>
svn log<br/>
<br/>
Referance:<br/>
https://www.tecmint.com/install-apache-subversion-svn-tortoisesvn-centos-debian-ubuntu/comment-page-2/?unapproved=1211100&moderation-hash=087d04eaf51a03dafce42b300168e45b#comment-1211100<br/>
