# omicloud
omicloud which implement linux machine management base on OMI

OMI:https://github.com/Microsoft/omi

Our omicloud is based on omi, and it can manage every Linux machine on the world which connected to Internet.

The first version of omicloud we need to implement a provider based on OMI.

Welcome everyone to join this project, thanks.


# Usage

Copy Cloud Folder to omi/Unix/samples/Providers
Build OMI from https://github.com/Microsoft/omi

Run below command to register Cloud provider
```
/root/omi/Unix/output/bin/omireg -o '@requestor@' -n root/cimv2 /root/omi/Unix/output/lib/libCloud.so

```

Run below command to collect tcp connection number,cpu,memory,disk usage data
```
/root/omi/Unix/output/bin/omicli ei root/cimv2 OMI_Cloud
instance of OMI_Cloud
{
    [Key] Id=1001
    Command=netstat|grep CONNECTED|wc -l
    Result=86

}
instance of OMI_Cloud
{
    [Key] Id=1002
    Command=top -bn1|grep load|awk '{printf "CPU Load:""%.2f", $(NF-2)}'
    Result=CPU Load:0.94
}
instance of OMI_Cloud
{
    [Key] Id=1003
    Command=free -m | awk 'NR==2{printf "Memory Usage:"$3","$2","$3*100/$2 }'
    Result=Memory Usage:314,992,31.6532
}
instance of OMI_Cloud
{
    [Key] Id=1004
    Command=df -h | awk '$NF=="/"{printf "Disk Usage:"$3"/"$2","$5}'
    Result=Disk Usage:2.5G/6.2G,41%
}
```
