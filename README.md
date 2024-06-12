# Sqlsystem-Stu-manager
数据库学生管理系统
改良的下面师傅的代码

- [student-management-system](https://github.com/ningzichun/student-management-system)
  功能如图
![image](https://github.com/Liaguone/Sqlsystem-Stu-manager/assets/142466110/bf342796-29fd-43ab-bb90-00578f30d517)
下拉式菜单页面
![image](https://github.com/Liaguone/Sqlsystem-Stu-manager/assets/142466110/b5f201db-d167-411b-8596-89717a165e3c)
美化新增学生页面
![image](https://github.com/Liaguone/Sqlsystem-Stu-manager/assets/142466110/83d2d253-fbd7-44b7-af2c-f7b3d48b880a)
院系管理
![image](https://github.com/Liaguone/Sqlsystem-Stu-manager/assets/142466110/21664b57-801f-4e78-a9bc-7313a4887a9d)

系统管理页面

![image](https://github.com/Liaguone/Sqlsystem-Stu-manager/assets/142466110/991bf07d-ff6f-41b4-84be-273253a79324)

剩下的学生系统页面
![image](https://github.com/Liaguone/Sqlsystem-Stu-manager/assets/142466110/da9e3f3f-1bf2-4194-a26b-96bec8e35da5)


解压得文件夹sqlsystem,将根目录放到phpstudy里面(安装建站自己搜教程噢)

config里面配置数据库(database文件)

建表

```sql
SET NAMES utf8;
SET time_zone = '+00:00';
SET foreign_key_checks = 0;
SET sql_mode = 'NO_AUTO_VALUE_ON_ZERO';

DROP TABLE IF EXISTS `course`;
CREATE TABLE `course` (
  `cid` char(6) DEFAULT NULL,
  `cname` varchar(15) DEFAULT NULL,
  `credit` decimal(2,1) DEFAULT NULL,
  `cadd` varchar(20) DEFAULT NULL,
  `did` char(2) DEFAULT NULL,
  `tname` varchar(15) DEFAULT NULL,
  UNIQUE KEY `cid_2` (`cid`),
  KEY `cid` (`cid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;


DROP TABLE IF EXISTS `department`;
CREATE TABLE `department` (
  `did` char(2) DEFAULT NULL,
  `dname` varchar(15) NOT NULL,
  `dadd` varchar(30) DEFAULT NULL,
  `dmng` varchar(10) DEFAULT NULL,
  `dtel` varchar(15) DEFAULT NULL,
  UNIQUE KEY `did_2` (`did`),
  KEY `did` (`did`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;


DROP TABLE IF EXISTS `major`;
CREATE TABLE `major` (
  `did` char(2) DEFAULT NULL,
  `mname` varchar(20) DEFAULT NULL,
  UNIQUE KEY `did_2` (`did`,`mname`),
  KEY `did` (`did`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;


DROP TABLE IF EXISTS `student`;
CREATE TABLE `student` (
  `sid` char(12) NOT NULL,
  `name` varchar(10) NOT NULL,
  `sex` char(1) NOT NULL,
  `age` varchar(3) DEFAULT NULL,
  `class` varchar(10) DEFAULT NULL,
  `idnum` char(18) DEFAULT NULL,
  `did` char(2) DEFAULT NULL,
  `email` char(30) DEFAULT NULL,
  `tel` char(11) DEFAULT NULL,
  PRIMARY KEY (`sid`),
  UNIQUE KEY `sid` (`sid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;


DROP TABLE IF EXISTS `student_course`;
CREATE TABLE `student_course` (
  `sid` char(12) NOT NULL,
  `cid` char(6) NOT NULL,
  `score` int(3) DEFAULT NULL,
  `status` char(1) DEFAULT NULL,
  KEY `sid` (`sid`),
  KEY `cid` (`cid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;


DROP TABLE IF EXISTS `student_log`;
CREATE TABLE `student_log` (
  `sid` varchar(12) DEFAULT NULL,
  `type` char(1) DEFAULT NULL,
  `reason` varchar(30) DEFAULT NULL,
  `detail` varchar(100) DEFAULT NULL,
  `logdate` date DEFAULT NULL,
  `addtime` datetime DEFAULT NULL,
  KEY `sid` (`sid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;


DROP TABLE IF EXISTS `user_admin`;
CREATE TABLE `user_admin` (
  `adminID` varchar(15) DEFAULT NULL,
  `adminName` varchar(15) DEFAULT NULL,
  `pwd` char(32) DEFAULT NULL,
  KEY `adminID` (`adminID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;


DROP TABLE IF EXISTS `user_student`;
CREATE TABLE `user_student` (
  `sid` char(12) NOT NULL,
  `pwd` char(32) DEFAULT NULL,
  UNIQUE KEY `sid` (`sid`),
  KEY `sid_2` (`sid`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

新建管理员账户，在表 user_admin 中新建一行记录，adminID 为管理员ID，adminName 为管理员姓名，pwd为MD5加密后的密码。 实例代码如下（通用的admin）：

```sql
INSERT INTO `user_admin` (`adminID`, `adminName`, `pwd`) VALUES
('admin', 'admin', '21232f297a57a5a743894a0e4a801fc3');
```
学院增加(没有添加增加学院的功能)
```sql
INSERT INTO `department` (`did`, `dname`, `dadd`, `dmng`, `dtel`) VALUES
('01', '电子信息学院', '中心公教楼106d', '刘德华', '13310001100'),
('02', '智能制造学院', '行知楼3301d', '刘德华', '13929298269'),
('03', '人文学院', '明知楼3301d', '刘德华', '13929298269'),
('04', '设计学院', '名苑楼3301d', '刘德华', '13929298269'),
('05', '马克思主义学院', '图灵科技楼201d', '刘德华', '13727524159');

剩下的功能如图

