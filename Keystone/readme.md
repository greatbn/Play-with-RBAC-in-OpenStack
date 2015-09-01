#1.Tạo user,tenant,role mới 
- Tạo user saphi có role VDC trong tenant VDC
 + tạo user

  `keystone user-create --name saphi --pass saphi`

<img src="http://i.imgur.com/RayBe64.png">

 + tạo tenant

   `keystone tenant-create --name VDC --description "VDC Tenant"`
 
<img src="http://i.imgur.com/zrLIBVE.png">

 + Tạo role

   `keystone role-create --name VDC`

<img src="http://i.imgur.com/d37ShkU.png">

 + Add user saphi vào role VDC và tenant VDC

   `keystone user-role-add --user saphi --role VDC --tenant VDC`

**Mặc định keystone chỉ user admin role admin mới có thể được sử dụng. Nhưng giờ ta sẽ cho user saphi với role VDC trong tenant VDC có thể sử dụng được keystone**

<img src="http://i.imgur.com/YS7chgg.png">

#2.Sửa file /etc/keystone/policy.json

- Dòng đầu tiên is_admin:1 

<img src="http://i.imgur.com/zK83KxQ.png">

- Thành: role:VDC

<img src="http://i.imgur.com/sbCNaVo.png">

- Không cần restart lại glance-api và glance-registry
- Đăng nhập với user saphi test
 + Tạo file saphi.sh với nội dung


```sh
export OS_USERNAME=saphi
export OS_PASSWORD=saphi
export OS_TENANT_NAME=VDC
export OS_AUTH_URL=http://10.10.10.71:35357/v2.0
```

- Chạy lệnh `source saphi.sh`

- Test lệnh `keystone user-list`

<img src="http://i.imgur.com/Dgsx1QP.png">

- Đã hoạt động 
