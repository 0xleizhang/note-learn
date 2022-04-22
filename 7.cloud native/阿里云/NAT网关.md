内网内VM可以都不绑定购买公网IP，通过NAT访问公网和被公网访问

关系的建立

网关关联了EIP,交换机 ；交换机属于VPC

VM关联了交换机

SNAT和DNAT的区别

SNAT: Source Network Address Translation

DNAT: Destination Network Address Translation

SNAT 内网VM访问外网

\`vm(client)--->SNAT(将数据包中的内网源IP转换为外网IP)--->Internet(服务器）--->SNAT(将数据包内的目的IP转换为内网IP)--->vm(client)\`

DNAT 外网能够访问内网VM

\`Internet(client用户)--->DNAT(将数据包中的目的公网IP转换为目的内网IP)--->VM(server)--->DNAT(将数据包中的源内网IP转换为外网IP)--->Internet(client用户)\`

DNAT是外网端口转发到内网VM端口