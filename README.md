![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 更改所有作业的所有者
#### Change Owner For All SQL Jobs
**发布-日期: 2014年05月09日 (评论)**

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
这是更改SQL Server代理中所有作业所有者的快速方法。假设你要将所有所有者设置为名为MyDomain \ SQL_AGT的SQL Server代理帐户。
你可以通过运行此简单的TSQL逻辑在所有作业中执行此操作。根据以下脚本你可以找到另一组用于检查哪些作业所有者已更改的逻辑。

## English
Here’s a quick way to change all the Job owners in SQL Server Agent. Lets say you want to set all the owners to the SQL Server Agent Account called MyDomain\SQL_AGT.
You can do this across all jobs by running this simple TSQL Logic. Following the script you can find another set of logic that will check to see which Job owners were changed.

---
## Logic
```SQL
use msdb;
set nocount on
declare @new_job_owner 		varchar(50)
declare @change_job_owners 	varchar(max)
set 	@new_job_owner = 'TP\SQL_AGT' --sql agent service account. set @change_job_owners = ''
select	@change_job_owners = @change_job_owners +
'use msdb; ' + char(10) + 'exec sp_update_job @job_name = ''' + name + ''',' + char(10) + '@owner_login_name = ''' + @new_job_owner + ''';' + char(10) + char(10)
from 
	msdb..sysjobs 
where 
	suser_name(owner_sid) not in ('MyDomain\SQL_AGT') -- change all owners that are not set to new job owner account. order by name asc
exec (@change_job_owners) --for xml path(''), type


```


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

