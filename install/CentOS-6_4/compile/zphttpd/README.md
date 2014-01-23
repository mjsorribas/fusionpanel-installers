Create rpm for zphttpd


<code>yum -y install pcre-devel lua-devel libxml2-devel --downloadonly --downloaddir=$HOME/rpmbuild/RPMS/$(uname -m)</code>

<code>yum -y install pcre-devel lua-devel libxml2-devel</code>

<code>wget https://github.com/zpanel/installers/raw/master/install/CentOS-6_4/compile/zphttpd/zphttpd.spec \ </code>

<code>-P $HOME/rpmbuild/SPECS</code>

<code>cd $HOME/rpmbuild/SOURCES</code>

<code>git clone https://github.com/apache/httpd.git httpd-2.4.7</code>

<code>cd httpd-2.4.7</code>

<code>git checkout 2.4.7</code>

<code>cd ..</code>

<code>tar cvjf httpd-2.4.7.tar.bz2 httpd-2.4.7</code>

<code>rm -rf httpd-2.4.7/</code>

<code>rpmbuild -ba $HOME/rpmbuild/SPECS/zphttpd.spec</code>

#Regenerate repo

<code>createrepo --update $HOME/rpmbuild/RPMS/$(uname -m)</code>

#Install

<code>sed -i 's/enabled=1/enabled=0/g' "/etc/yum.repos.d/CentOS-Media.repo"</code>

<code>yum -y update</code>

<code>sed -i 's/enabled=0/enabled=1/g' "/etc/yum.repos.d/CentOS-Media.repo"</code>

<code>yum -y update</code>

<code>yum -y install zphttpd</code>