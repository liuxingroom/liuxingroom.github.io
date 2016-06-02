---
layout: post
title:  "Hibernate 级联操作 !"
date:   2016-06-02 14:24:16 +0800
categories: jekyll update
---
#Hibernate 中的级联操作
以用户、角色、用户文件为例讲解inverse（关系操作）和（cascade）操作
inverse 取值 true（不维护关系）或false（维护关系  默认为false） 该属性主要操作的是外键
cascade 取值null（默认值）、save-update 、all 、delete
用户、角色是多对多的关系
用户的映射文件表示：
<hibernate-mapping>
<class name="com.xing.elec.domain.ElecUser" table="Elec_User">
。。。。。
<set name="elecUserFiles" table="Elec_User_File" inverse="true" order-by="progressTime desc"  cascade="delete">
<key>
<column name="userID"></column>
</key>
<one-to-many class="com.xing.elec.domain.ElecUserFile"/>
</set>
<set name="elecRoles" table="elec_user_role" inverse="true">
<key>
<column name="userID"></column>
</key>
<many-to-many class="com.xing.elec.domain.ElecRole" column="roleID"></many-to-many>
</set>
</class>
</hibernate-mapping>
角色的映射文件：
<hibernate-mapping>
<class name="com.xing.elec.domain.ElecRole" table="Elec_Role">
。。。。
<set name="elecUsers" table="elec_user_role">
<key>
<column name="roleID"></column>
</key>
<many-to-many class="com.xing.elec.domain.ElecUser" column="userID"/>
</set> 
</class>
</hibernate-mapping>
关系操作：
事例一：
由于用户和用户文件建立关联的set标签中 的inverse 设置为true 因此用户和用户文件之间建立的关系（外键）由用户文件来维护
比如说在 新增用户时一个用户有多个用户文件  在向数据库添加插入数据前要执行  elecUserFile.setElecUser(elecUser);该行代码
改行代码的作用是将用户和用户文件建立关联关系  即（当用户和用户文件的数据插入数据库时 用户文件表中对应的外键有值）
事例二：
由于用户和角色（即：用户表）建立关联的set标签中的inverse设置值为true    而角色用户（即：角色表）建立的关联的set标签设置为inverse="false"(默认为false) 则：
在删除用户时要删除用户和角色的关联关系（用户角色表中的相关数据） 
 如果用用户来删除用户角色表中相关的数据   该操作会报一个异常（存在外键不能删除的异常）
  正确做法： 是通过用户来获取该用户所有的角色（set集合）然后遍历该set集合得到该用户的每个角色  通过角色在获取用户的set集合  然后在删除该用户
（使用角色来删除用户角色表中的数据 其实也就是使用角色来操作外键）
代码实现：
Set<ElecRole> elecRoles=user.getElecRoles();
if(elecRoles!=null && elecRoles.size()>0){
for(ElecRole elecRole:elecRoles){
//(通过角色获取封装用户的set集合   来删除用户)
elecRole.getElecUsers().remove(user);
}
}

级联操作
事例一：
条件：由于用户和用户文件建立关联的set标签中 cascade设置为delete 
结果： 当删除用户信息时 与该用户有关的用户文件信息都会被删除（这属于级联删除操作）
总结：
inverse： 用来维护关系  一般我们用多的一方来维护一的一方（这样效率高） 而用一的一方来维护多的一方（这样执行的效率不好）
cascade：主要用于一对一  和一对多   多对多不建议使用
多对多不建议使用cascade 的原因（以用户角色为例）：如果删除一个用户 就会删除用户表关联的用户角色表以及角色表中相关的数据 而角色表中的数据不应该删除
---
[Code on GitHub](https://github.com/liuxingroom/liuxingroom.github.io)
[我的技术博客](http://blog.csdn.net/zcl1199/article/details/51366824)
---
