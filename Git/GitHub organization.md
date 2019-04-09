# GitHub 实现多人协同提交代码并且权限分组管理

### 0、创建组织优缺点
其优点是：操作简单，快速上手。
缺点是：没有办法实现权限控制。
为啥要权限控制？这是一个蛋疼的问题
因为我们为了项目的安全考虑，需要对一部分人开放只读权限(只能 read、clone) ; 
或者对一部分人开放写权限(只能 read、clone、push) ; 
或者对一部分人开放管理者权限(只能 read、clone、push、给仓库添加成员 )。
事实上github对权限的管理只有4种，前三种权限分别是 Admin(管理者)、Write(只写) 、Read(只读) 。
最后一种权限比较特殊，它是该组织的创建者，拥有至高无上的的权利。
<br><br><br>

### 1、github实战--创建组织

生意人可以创建项目和组织。对应到github上的用户可以创建仓库和组织。
![blockchain](https://images2015.cnblogs.com/blog/605655/201609/605655-20160919134451262-1641512058.png '1')
![blockchain](https://images2015.cnblogs.com/blog/605655/201609/605655-20160919135811152-676430683.png '2')
![blockchain](https://images2015.cnblogs.com/blog/605655/201609/605655-20160919135831887-796744077.gif '3')

### 2、github实战--在组织中创建仓库
当创建完组织后，来看看组织的结构
![blockchain](https://images2015.cnblogs.com/blog/605655/201609/605655-20160919140654590-1651498572.png '4')
在Organ-Name 组织下，创建一个仓库
![blockchain](https://images2015.cnblogs.com/blog/605655/201609/605655-20160919141042527-1718710011.gif '5')

### 3、github实战--在组织中创建team
![blockchain](https://images2015.cnblogs.com/blog/605655/201609/605655-20160919141552606-1805098616.gif '6')
 团队创建完成后，默认这个团队的成员只有一个人，就是该账号。下面就开始给这个team添加其他成员。
![blockchain](https://images2015.cnblogs.com/blog/605655/201609/605655-20160919143047918-225222184.gif '7')
邀请成功以后，需要被邀请人去自己的邮箱点击一下，确认邀请

### 4、github实战--在组织中给仓库添加team并且设置权限。
![blockchain](https://images2015.cnblogs.com/blog/605655/201609/605655-20160919145301793-2066352342.gif '8')
可以看到，仓库对team的权限控制有三种

    Admin 管理者权限(只能 read、clone、push、给仓库添加成员 )
    Write 写权限(只能 read、clone、push)
    Read 读权限(只能 read、clone) 

另外任意一个Team可以供多个组织使用，到这里权限添加已经全部完成了。

### 总结
  通过这篇文章可以在github愉快的使用权限管理了，但是github不能免费的创建私有仓库，这是一个很严重的问题。如果是开源项目，用github完全没有问题。如果是私有项目，可以有以下几个途径达到要求
  
    1、在github花钱购买私有仓库。
    2、使用国内比较出名的开源中国git托管服务：https://git.oschina.net/   
    3、使用GitLab,这需要在自己的服务器上部署。传送门：https://about.gitlab.com/gitlab-com/
