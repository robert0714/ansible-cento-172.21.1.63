#ansible-playbook  common.yml  -i hosts/all
更換yum repository
 ==============
 記得要下yum clean all，或著照提示做rm -rf /var/cache/yum
 
 
 在使用yum時，會將下載的東西，存放在/var/cache/yum目錄下。
1.yum更新
yum check-update
#檢查能更新的套件有那些

yum update
#更新所有已安裝的套件，若在update後面接上套件名稱的話可針對該套件更新
如yum update httpd

yum upgrade
#功能看update差不多，差別在於yum upgrade會連同一些過舊即將洮汰的套件也一起更新，大多使用在版本升級。

1.1安裝移除套件
yum install
#安裝套件，install後面接要安裝的套件名稱，如yum install httpd。若要把所有相關的一起安裝的話可在最後加上「*」。如yum install httpd*

yum remove
#移除套件在這邊會考慮到相依性的問題，remove後可接要移除套件名稱，如yum remove httpd。若要把相關套件也一起移除的話可在最後加上「*」。如yum remove httpd*

yum clean
#清除安裝下載時的暫套件原始檔，大多是存放在/var/cache/yum，通常會下yum clean packages或是yum clean all，一次全刪除。

1.2清暫存
yum clean
#清除安裝下載時的暫套件原始檔，大多是存放在/var/cache/yum

yum clean packages
#用來清除暫存(/var/cache/yum)目錄下的套件

yum clean headers
#用來清除暫存(/var/cache/yum)目錄下的 headers

yum clean oldheaders
#用來清除暫存(/var/cache/yum)目錄下的 oldheaders

yum clearn all
#直接把所有的站存都一次清除。

1.3列清單
yum list
#列出所有的套件，若在list後面接套件名稱，則可單獨列出該套件。

yum list updates
#列出所有可以更新的套件

yum list installed
#列出所有已經安裝的套件

yum list extra
#列出所有已安裝但不在 yum Repository 內的套件

1.4列出套件的相關資訊
yum info
#列出所有套件的相關資訊，若在info後接上套件名稱，則可單讀該套件相關資訊。
如yum info httpd 或yum info httpd*，差別在於有加「*」則會把以httpd開頭的都列出來

yum info updates
#列出所有可以更新的套件資訊

yum info installed
#列出所有已安裝的套件資訊

yum info extras
#列出所有已安裝但不在 Yum Repository 內的套件資訊

1.5搜尋功能
yum search
#搜尋所有相關的套件，如yum search httpd，在從中找到所需要的套件。類似關鍵字的用途

五、升級不動kernel
如果想要用yum來升級套件，但又不想動到kernel的話。請參考下面做法
[root@localhost ~]# vim /etc/yum.conf
#在[main]當中加入下面字串
exclude=kernel kernel-source
