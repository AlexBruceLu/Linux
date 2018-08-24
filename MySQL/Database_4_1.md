## go操作MySQL小Deom

### Deom背景简介

游戏数据来源于数据库，数据库中分别有如下几张表：


##### 1、	hero表，表中记录玩家可选英雄以及英雄属性

##### 2、	weapon表，该表中记录玩家可购买的武器，以及武器的属性

##### 3、	monster表，该表记录玩家的敌人以及敌人属性

##### 4、	player表，该表记录具体玩家的信息

#### 游戏流程如下：

**首先提示用户从hero表中的英雄里选取一个英雄进行游戏，当玩家选择英雄后提示玩家所选英雄，并且给玩家选择界面，
选择界面主要包括：战斗、查看玩家资料、购买武器以及退出游戏。**


**战斗模块：玩家可以从monster表中所有的怪物里自行选择一个挑战，如果战斗胜利，获取经验、金钱，如果失败，退出游戏。**


**查看资料模块：查看当前玩家资料、包括玩家当前的姓名、武器、金钱、攻击力、防御力以及血量。**


**购买武器：购买武器时只显示比玩家当前武器高一级的武器可以进行购买，如果购买的最强的武器，再次选择该功能，
提示武器已经为最强，并且自动返回到选择界面。**


**退出游戏：玩家可以主动退出游戏。**


### 数据库准备


**1.创建游戏数据库GameDatabase，在该数据库下创建实现各个模块功能的表。**


**2.创建hero表：**


```sql
CREATE TABLE
IF NOT EXISTS hero (
    heroId INT PRIMARY KEY,    -- 英雄编号 主键
    heroName VARCHAR (20),     -- 英雄姓名
    heroATK INT ,              -- 英雄初始攻击力
    heroDEF INT ,              -- 英雄初始防御力
    heroHP  INT ,              -- 英雄初始血量
    heroAddATK INT ,           -- 英雄每级提升攻击力
    heroAddDEF INT ,           -- 英雄每级提升防御力
    heroAddHP   INT,           -- 英雄每级提升血量
    heroInfo VARCHAR(30)       -- 英雄简介
);
```

**3.创建weapon表：**

```sql
CREATE TABLE
IF NOT EXISTS weapon (
  weaponId INT  PRIMARY KEY,  	  -- 武器编号
  weaponName VARCHAR(20),         -- 武器名称
  weaponATK  INT,                 -- 武器攻击力
  weaponCritRate INT,             -- 武器暴击率
  weaponCritPlus INT,             -- 武器暴击系数
  weaponForzenRate INT,           -- 武器冰冻率
  weaponMoney  INT                -- 武器价值
);
```

**4.创建monster表：**

```sql
CREATE TABLE
IF NOT EXISTS monster (
  monsterId INT  PRIMARY KEY,  	   -- 怪物编号
  monsterName VARCHAR(20),         -- 怪物名称
  monsterAtk  INT,                 -- 怪物攻击力
  monsterDEF INT,                  -- 怪物防御力
  monsterHP  INT,                  -- 怪物血量
  monsterMinMoney INT,             -- 怪物掉落最少金钱
  monsterMaxMoney INT              -- 怪物掉落最多金钱
);
```

**5.创建player表**

```sql
CREATE TABLE
IF NOT EXISTS player (
  heroId INT  PRIMARY KEY,   -- 英雄编号
  weaponId  INT,             -- 英雄武器编号
  heroLevel INT,             -- 英雄等级
  heroExp   INT,             -- 英雄经验
  money     INT              -- 英雄获得的金钱
);
```

***效果图***

 ![image](https://raw.githubusercontent.com/wiki/AlexBruceLu/Linux/MySQL_4.png)
