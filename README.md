yum update -y
yum update && yum install mod_dav_svn subversion httpd -y
vim /etc/httpd/conf.modules.d/10-subversion.conf 
mkdir /opt/svn
htpasswd -cB /etc/httpd/subversion-auth svn
chgrp apache /etc/httpd/subversion-auth
chmod 660 /etc/httpd/subversion-auth
firewall-cmd --add-service=http --permanent
firewall-cmd --reload 
svnadmin create /opt/svn/trun
chown -R apache:apache /opt/svn/trun
chcon -R -t httpd_sys_content_t  /opt/svn/trunk
chown -R apache:apache /opt/svn/trunk
chcon -R -t httpd_sys_content_t  /opt/svn/trunk
vim /etc/sysconfig/selinux -Try with SELLINUX dsiabled if not make enable of SELINUX
Optional step-> chcon -R -t httpd_sys_content_t  /opt/svn/trunk
Optional step-> chcon -R -t httpd_sys_rw_content_t /opt/svn/trunk
systemctl restart httpd

Open Browser
http://ip:80/svn/trunk

Referance:
https://www.tecmint.com/install-apache-subversion-svn-tortoisesvn-centos-debian-ubuntu/comment-page-2/?unapproved=1211100&moderation-hash=087d04eaf51a03dafce42b300168e45b#comment-1211100
