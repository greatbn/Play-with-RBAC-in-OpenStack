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

**Mặc định glance sẽ cho tất cả các user có thể add image nhưng giờ ta sẽ không cho user saphi trong role VDC upload image lên nữa và chỉ role admin có được quyền này**

<img src="http://i.imgur.com/lkYzwuU.png">

#2.Sửa file /etc/glance/policy.json

- sửa dòng `"add_image": ""` thành  `"add_image": "role:admin"`

<img src="http://i.imgur.com/o0Pzvzs.png">

- Như sau

<img src="http://i.imgur.com/iFy81s8.png">

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

- Test lệnh 

`glance image-create --name "DEMO" --disk-format qcow2 --container-format bare --is-public True --progress < cirros-0.3.4-x86_64-disk.img`

<img src="http://i.imgur.com/z3Jh6bQ.png">
- Đã hoạt động 
- Đăng nhập user admin kiểm tra các image
`glance image-list`

<img src="http://i.imgur.com/7Ffeg0g.png">