#1.T?o user,tenant,role m?i 
- T?o user saphi c� role VDC trong tenant VDC
 + t?o user

  `keystone user-create --name saphi --pass saphi`

<img src="http://i.imgur.com/RayBe64.png">

 + t?o tenant

   `keystone tenant-create --name VDC --description "VDC Tenant"`
 
<img src="http://i.imgur.com/zrLIBVE.png">

 + T?o role

   `keystone role-create --name VDC`

<img src="http://i.imgur.com/d37ShkU.png">

 + Add user saphi v�o role VDC v� tenant VDC

   `keystone user-role-add --user saphi --role VDC --tenant VDC`

**M?c d?nh keystone ch? user admin role admin m?i c� th? du?c s? d?ng. Nhung gi? ta s? cho user saphi v?i role VDC trong tenant VDC c� th? s? d?ng du?c keystone**

<img src="http://i.imgur.com/YS7chgg.png">

#2.S?a file /etc/keystone/policy.json

- D�ng d?u ti�n is_admin:1 

<img src="http://i.imgur.com/zK83KxQ.png">

- Th�nh: role:VDC

<img src="http://i.imgur.com/sbCNaVo.png">

- Kh�ng c?n restart l?i glance-api v� glance-registry
- �ang nh?p v?i user saphi test
 + T?o file saphi.sh v?i n?i dung


```sh
export OS_USERNAME=saphi
export OS_PASSWORD=saphi
export OS_TENANT_NAME=VDC
export OS_AUTH_URL=http://10.10.10.71:35357/v2.0
```

- Ch?y l?nh `source saphi.sh`

- Test l?nh `keystone user-list`
<img src="http://i.imgur.com/Dgsx1QP.png">
- �� ho?t d?ng 
