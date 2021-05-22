https://blog.csdn.net/liumiaocn/article/details/78877957

https://www.jianshu.com/p/9a267a837736


参考第一个链接完成除最后一步外的前面步骤。
最后使用第二个链接中的
sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv


 1794  df -h
 1795  lsblk
 1796  fdisk -l
 1797  sudo fdisk -l
 1798  fdisk /dev/sda
 1799  sudo fdisk /dev/sda
 1800  lsblk
 1801  fdisk -l
 1802  sudo fdisk -l
 1803  partprobe
 1804  sudo partprobe
 1805  sudo fdisk -l
 1806  lsblk
 1807  vsg
 1808  vgs
 1809  suod vgs
 1810  sud vgs
 1811  sudo vgs
 1812  pvcreate /dev/sda3
 1813  sudo pvcreate /dev/sda3
 1814  sudo pvcreate /dev/sda3 -ff
 1815  lsblk
 1816  ls /
 1817  ls
 1818  ls sandbox/
 1819  sudo pvcreate /dev/sda4
 1820  vgs
 1821  sudo vgs
 1822  vgextend ubuntu-vg /dev/sda4
 1823  suod vgextend ubuntu-vg /dev/sda4
 1824  sudo vgextend ubuntu-vg /dev/sda4
 1825  sudo vgs
 1826  lvs
 1827  sudo lvs
 1828  lslbk
 1829  lsblk
 1830  sudo lvs
 1831  lvextend /dev/ubuntu-vg/ubuntu-lv /dev/sda4
 1832  sudo lvextend /dev/ubuntu-vg/ubuntu-lv /dev/sda4
 1833  suod lvs
 1834  sudo lvs
 1835  df -h
 1836  lsblk
 1837  sudo reboot
 1838  df -h
 1839  lsblk
 1840  df -hT
 1841  resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
 1842  sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
 1843  lsblk
 1844  df -h
 1845  ls /
 1846  fdisk -l
 1847  sudo fdisk -l
 1848  history