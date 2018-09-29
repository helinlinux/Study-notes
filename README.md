# Study-notes
This is my study notes.

subversion control SVN版本控制

1. install the subversion

2.Create version library 创建版本库
  mkdir /var/svn
  svnadmin create /var/svn/project
  
3.Import project code #导入项目代码
  cd /usr/lib/systemd/system
  svn import ./ file:///var/svn/project -m "instructions" # instructions 使用说明
  
 4.Modify the file of configure.
  vim /var/svn/project/conf/serve.conf
    line 19: anon-access = none  #屏蔽匿名用户
    line 20: auth-access = write #认证用户读写
    line 27: password-db = passwd #密码文件
    line 34: authz-db =authz      #acl访问控制列表文件
    
  vim /var/svn/project/conf/passwd
    ....
    [users]
     tom = 123456
     jerry = 123456
     .....
    
   vim /var/svn/project/conf/authz
     .....
     [/]
     tom = rw
     harry =rw
     
   5.Start the service.
      svnserve -d -r /var/svn/project
      
   6.The client download
     cd /tmp
     svn --username tom --password 123456 co svn://192.168.2.100/ code #co = checkout 
