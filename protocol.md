# 路由器web交互接口协议数据格式

TODO:
- 数据格式的校验全部由前端做
- 时间单位统一为秒
- 绝对时间统一为utc时间
- 流量的单位统一为KB
- mac地址统一为16进制小写不带冒号
- 所有的整数或者浮点数都为本身，不定义成字符串
- 获取日志直接拉取日志文件，日志文件名称叫router.log


# 前端和路由器交互请求
- method : json字符串
- 发送的全是post方法

json字符串结构
``` json
{
    "request" : "XXX",  //可选字段，web界面下发时有效，调用的接口名
    "parameter" : ""//结果和请求参数都通过该字段下发  可选字段，如果没有返回参数，则没有该字段
    "code" : "XX" //错误码，可选字段，web界面返回有效
}
```

# i'm hear
- 升级，配置文件接口还未定

---
---

- [login](#login)
- [set_router_mode](#set_router_mode)
- [get_router_mode](#get_router_mode)
- [get_router_info](#get_router_info)
- [set_timer_restart](#set_timer_restart)
- [get_timer_restart_info](#get_timer_restart_info)
- [router_operation](#router_operation)
- [set_admin_password](#set_admin_password)
- [get_repeater_wifi_info](#get_repeater_wifi_info)
- [set_repeater](#set_repeater)
- [get_device_info](#get_device_info)
- [get_mesh_node_info](#get_mesh_node_info)
- [get_wan_network](#get_wan_network)
- [set_wifi](#set_wifi)
- [get_wifi_info](#get_wifi_info)
- [set_wifi_power](#set_wifi_power)
- [set_guest_wifi](#set_guest_wifi)
- [get_guest_wifi_info](#get_guest_wifi_info)
- [set_lan](#set_lan)
- [get_lan_info](#get_lan_info)
- [set_smb](#set_smb)
- [get_smb_info](#get_smb_info)
- [get_camera_storage_info](#get_camera_storage_info)
- [set_camera_storage](#set_camera_storage)
- [set_clouddisk](#set_clouddisk)
- [get_clouddisk_info](#get_clouddisk_info)
- [set_dlan](#set_dlan)
- [get_dlan_info](#get_dlan_info)
- [add_blacklist_node](#add_blacklist_node)
- [del_blacklist_node](#del_blacklist_node)
- [update_blacklist_nod](#update_blacklist_nod)
- [get_blacklist_info](#get_blacklist_info)
- [add_rsvd_node](#add_rsvd_node)
- [del_rsvd_node](#del_rsvd_node)
- [update_rsvd_node](#update_rsvd_node)
- [get_rsvd_info](#get_rsvd_info)
- [add_portfw_node](#add_portfw_node)
- [del_portfw_node](#del_portfw_node)
- [update_portfw_node](#update_portfw_node)
- [get_portfw_info](#get_portfw_info)
- [set_beaforming](#set_beaforming)
- [set_firewall](#set_firewall)
- [get_firewall_info](#get_firewall_info)
- [set_net_diagnosis](#set_net_diagnosis)
- [set_timezone](#set_timezone)
- [get_timezone](#get_timezone)

---
---

### general_result
``` json
"code" : "" //错误码
```

### wifi_node_info
``` json
{
    //可选字段，没有的话代表不设置
    "enabled" : "true"/"false",
    "mac" : "XXX",
    "hidden" : "true"/"false",
    "ssid" : "XXX",
    "mode" : "", //2.4g:bgn   5g://anac
    "passwd" : "XXX",
    "channel" : "XXX",
    "encryption" : "open"/"wap/wpa2"
}
```
---
---

### login
``` json
{
    "passwd" : "xxxxxx"
}
```
#### [jump to general_result](#general_result)


### set_router_mode
``` json
{
    "mode" : "router"/"repeater"
}
```
#### [jump to general_result](#general_result)

### get_router_mode
``` json
{
    "mode" : "router"/"repeater"
}
```

### get_router_info
``` json
{
    "mode" : "router"/"repeater",
    "duration" : 3600,
    "hardware_version" : "XXX",
    "firmware_version" : "XXX",
}
```

### set_admin_password
``` json
{
    "original_password" : "XXX",
    "new_password" : "XXX"
}
```
#### [jump to general_result](#general_result)

### router_operation
``` json
{
    "operation" : "reboot"/"reset"
}
```
#### [jump to general_result](#general_result)

### set_timer_restart
``` json
{
    "enabled" : "true"/"false",
    "time" : 36000
}
```
#### [jump to general_result](#general_result)

### get_timer_restart_info
``` json
{
    "enabled" : "true"/"flase",
    "time" : 36000
}
```

### get_repeater_wifi_info
``` json
{
    "list" : 
    [
        {
            "band" : "5g",
            "ssid" : "XXX",
            "rssi" : 20
        },
        {
            "band" : "2.4g"
            "ssid" : "XXX",
            "rssi" : 20
        }
    ]
}
```

### set_repeater
``` json
{
    "ssid" : "XXX",
    "passwod" : "XXX"
}
```
#### [jump to general_result](#general_result)


### get_wan_status
``` json
{
    "result" : "ulink"/"link"/"unconnect"/"connect",//(插上网线/未插网线/能够上网/不能够上网)
    "access_time" : 3600 //单位s
}
```

### get_wan_network
``` json
{
    "network_mode" : "dhcp"/"static"/"pppoe",
    "speedup" : 1024,
    "speeddown" : 1024,

    //如果是static
    "ipaddr" : "XXX",
    "subnet_mask" : "XXX",
    "gateway" : "XXX",
    "dns":
    [
        {
            "dns1" : "XXX"
        },
        {
            "dns2" : "XXX" //可选
        }
    ],

    //如果是pppoe
    "username" : "XXX",
    "password" : "XXX",

    //如果是dhcp
    "dns":
    [
        {
            "dns1" : "XXX"
        },
        {
            "dns2" : "XXX" //可选
        }
    ]
}
```

### set_wan_network
``` json
{
    "network_mode" : "dhcp"/"static"/"pppoe",
    "static_info":
    {
        "ipaddr" : "XXX",
        "subnet_mask" : "XXX",
        "gateway" : "XXX",
        "dns":  //可选字段
        [
            "dns1" : "XXX",
            "dns2" : "XXX",
        ]
    },
    "dhcp_info" :   //可选字段
    {
        "dns1" : "XXX",
        "dns2" : "XXX"
    },
    "pppoe_info" : 
    {
        "username" : "XXX",
        "password" : "XXX",
    }
}
```
#### [jump to general_result](#general_result)


### set_lan
``` json
{
    "ipaddr" : "XXX",
    "subnet_mask" : "XXX",
    "ip_start" : "XXX",
    "ip_end" : "XXX"
}
```
#### [jump to general_result](#general_result)

### get_lan_info
``` json
{
    "mac" : "XXX",
    "ipaddr" : "XXX",
    "subnet_mask" : "XXX",
    "ip_start" : "XXX",
    "ip_end" : "XXX"
}
```

### set_wifi
{
    "2.4g":
    {
        [jump to wifi_node_info](#wifi_node_info)
    },
    "5g":
    {
        [jump to wifi_node_info](#wifi_node_info)
    }
}
#### [jump to general_result](#general_result)

### get_wifi_info
{
    "2.4g":
    {
        [jump to wifi_node_info](#wifi_node_info)
    },
    "5g":
    {
        [jump to wifi_node_info](#wifi_node_info)
    }
}

### set_wifi_power
``` json
{
    "2.4g" : 100,
    "5g"   : 100
}
```

### set_guest_wifi
{
    "2.4g":
    {
        [jump to wifi_node_info](#wifi_node_info)
    },
    "5g":
    {
        [jump to wifi_node_info](#wifi_node_info)
    }
}
#### [jump to general_result](#general_result)

### get_guest_wifi_info
{
    "2.4g":
    {
        [jump to wifi_node_info](#wifi_node_info)
    },
    "5g":
    {
        [jump to wifi_node_info](#wifi_node_info)
    }
}

### get_device_info
``` json
{
    "num" : "XXX",
    "list" :
    [
        {
            "name" : "XXX",
            "id" : 1,
            "band" : "5g"/"2.4g",
            "mac" : "XXX",
            "timelimit" :
            {
                "start_time" : 100000, //utc时间s
                "end_time" : 100000, //utc时间s
                "day" : "sun|mon|tue|wed|thu|fri|sat",
                "timelimit_enable" : "true"/"flase"
            },
            "urllimit":
            {
                "urllimit_enabled" : "true"/"flase",
                "urllist" :
                [
                    {
                        "url" : "XXX"
                    },
                    {
                        "url" : "XXX"
                    }
                ]
            }
        }
    ]
}
```

### get_mesh_node_info
``` json
{
    "iptv_vlan_num" : "XXX",
    "dev_info" :
    [
        {
            "name" : "XXX",
            "mac" : "XXXX", //16进制小写
            "ip" : "192.168.1.100",
            "duration" : 3600,   //单位s
            "firmware_version" : "XXX",
            "iptv_enabled" : "true"/"false",
            "beamforming" : "true"/"false"
        },
        {
            "name" : "XXX",
            "mac" : "XXXX", //16进制小写
            "ip" : "192.168.1.100",
            "duration" : 3600,   //单位s
            "firmware_version" : "XXX",
            "iptv_enabled" : "true"/"false",
            "beamforming" : "true"/"false"
        }
    ]
}
```

### set_smb
``` json
{
    "pop-up" : "true"/"false", //可选字段，需要弹出的时候才设置
    //可选字段，和pop-up互斥
    "root_passwod" : "XXX",
    "guest_info" :
    {
        "name" : "XXX",
        "passwd" : "XXX",
        "privilege" : "read"/"read|write", //读/读写
        "enabled" : "true"
    }
}
```
#### [jump to general_result](#general_result)

### get_smb_info
``` json
{
    "capacity" : 1024, //单位M
    "residual" : 512, //单位M
    "root_passwod" : "XXX",
    "guest_info" :
    {
        "name" : "XXX",
        "passwd" : "XXX",
        "privilege" : "read"/"read|write",
        "enabled" : "true"
    }
}
```

### set_camera_storage
``` json
{
    "enabled" : "true"/"false"
}
```
#### [jump to general_result](#general_result)

### get_camera_storage_info
``` json
{
    "enabled" : "true"/"false"
}
```

### set_clouddisk
``` json
{
    "enabled" : "true"/"false",
    "username" : "XXX",
    "password" : "XXX",
    "speeddown_limit" : 1024, //限速的单位为KB  0为不限制
    "speedup_limit" : 1024, //限速的单位为KB    0为不限制
    "timelimit_enabled" : "true"/"false", 
    "start_time" : 1000000, //utc时间的秒数
    "end_time" : 1000000, //utc时间的秒数
    "day" : "sun|mon|tue|wed|thu|fri|sat",
}
```
#### [jump to general_result](#general_result)

### get_clouddisk_info
``` json
{
    "enabled" : "true"/"false",
    "username" : "XXX",
    "password" : "XXX",
    "speeddown_limit" : 1024, //限速的单位为KB
    "speedup_limit" : 1024, //限速的单位为KB
    "timelimit_enabled" : "true"/"false",
    "start_time" : 1000000, //utc时间的秒数
    "end_time" : 1000000, //utc时间的秒数
    "day" : "sun|mon|tue|wed|thu|fri|sat",
}
```

### set_dlan
``` json
{
    "enabled" : "true"/"false"
}
```
#### [jump to general_result](#general_result)

### get_dlan_info
``` json
{
    "enabled" : "true"/"false"
}
```

### add_blacklist_nod
``` json
{
    "mac" : "XXX",
    "name" : "XXX",
}
```
#### [jump to general_result](#general_result)

### del_blacklist_nod
``` json
{
    "list" :
    [
        "mac" : "XXX",
    ]
}
```
#### [jump to general_result](#general_result)

### update_blacklist_nod
``` json
{
    "list":
    [
        {
            "name" : "XXX",
            "mac" : "XXX"
        },
        {
            "name" : "XXX",
            "mac" : "XXX"
        }
    ]
}
```
#### [jump to general_result](#general_result)

### get_blacklist_info
``` json
{
    "list" :
    [
        {
            "name" : "XXX",
            "mac" : "XXX"
        },
        {
            "name" : "XXX",
            "mac" : "XXX"
        }
    ]
}
```

### add_rsvd_node
``` json
{
    "name" : "XXX",
    "mac" : "XXX",
    "ipaddr" : "XXX"
}
```
#### [jump to general_result](#general_result)

### del_rsvd_node
``` json
{
    "list":
    [
        {
            "mac" : "XXX"
        },
        {
            "mac" : "XXX",
        },
        {
            "mac" : "XXX"
        }
    ]
}
```
#### [jump to general_result](#general_result)


### update_rsvd_node
``` json
{
    "list":
    [
        {
            "name" : "XXX",
            "mac" : "XXX",
            "ipaddr" : "XXX"
        },
        {
            "name" : "XXX",
            "mac" : "XXX",
            "ipaddr" : "XXX"
        }
    ]
}
```
#### [jump to general_result](#general_result)

### get_rsvd_info
``` json
{
    "num" : 4,
    "list" :
    [
        {
            "name" : "XXX",
            "mac" : "XXX",
            "ipaddr" : "XXX"
        }
    ]
}
```

### add_portfw_node
``` json
{
    "ipaddr" : "XXX",
    "external_port" : "XXX",
    "internal_port" : "XXX",
    "protocol" : "tcp"/"udp"/"tcp&udp"
}
```
#### [jump to general_result](#general_result)

### del_portfw_node
``` json
{
    "list":
    [
        {
            "id" : 1,
        },
        {
            "id" : 2,
        }
    ]
}
```
#### [jump to general_result](#general_result)

### update_portfw_node
``` json
{
    "list":
    [
        {
            "id" : "XXX",
            "ipaddr" : "XXX",
            "external_port" : "XXX",
            "internal_port" : "XXX",
            "protocol" : "tcp"/"udp"/"tcp&udp"
        }
    ]
}
```
#### [jump to general_result](#general_result)

### get_portfw_info
``` json
{
    "num" : 10,
    "list":
    [
        {
            "id" : 1,
            "ipaddr" : "XXX",
            "external_port" : "XXX",
            "internal_port" : "XXX",
            "protocol" : "tcp"/"udp"/"tcp&udp"
        }
    ]
}
```

### set_beaforming
``` json
{
    "enabled" : "true"/"flase"
}
```
#### [jump to general_result](#general_result)

### set_firewall
``` json
{
    "icmp_enabled" : "true"/"false",
    "tcp_enabled" : "true"/"false",
    "udp_enabled" : "true"/"false"
}
```
#### [jump to general_result](#general_result)

### get_firewall_info
``` json
{
    "icmp_enabled" : "true"/"false",
    "tcp_enabled" : "true"/"false",
    "udp_enabled" : "true"/"false"
}
```

### set_net_diagnosis
``` json
{
    "type" : "ping"/"tracert",
    "host" : "www.baidu.com"
}
```
``` json
{
    "msg" : "XXXXXX"
}
```

### set_timezone
``` json
{
    "timezone" : "XXX",
}
```
#### [jump to general_result](#general_result)


### get_timezone
``` json
{
    "timezone" : "XXX",
    "issyn" : "true"/"false",
    "data" : 1000000
}
```

### set_remote_assist
``` json
{
    "enable" : "true"/"false"
}
```
#### [jump to general_result](#general_result)

### get_remote_assist
``` json
{
    "enable" : "true"/"false"
}
```
