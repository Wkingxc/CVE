SQL injection vulnerability exists in ibos oa v4.5.5

official website:http://www.ibos.com.cn/

version:4.5.5

Function point: Integrated Office = "Notification Announcement =" Mobile notification

![](https://s2.loli.net/2023/07/21/L9jm5PTSaEZG6nM.png)

POC

Routing: r = officialdoc officialdoc/edit

Successfully burst the database name by reporting an error injection

![](https://s2.loli.net/2023/07/21/LM2QpZPr5xAot7j.png)

Analyze

It's routed here and it calls the actionEdit() method, it selects the function point by passing in the op parameter and it calls move()
![image-20230721123330458](https://s2.loli.net/2023/07/21/OnglQsLMCY3ecAd.png)

Two arguments docids and catid are passed in the move() method where docids is injected, bringing the values of both arguments into the updateAllCatidByDocids() method.

![image-20230721123441984](https://s2.loli.net/2023/07/21/qYNXGkuevClUa9D.png)

The SQL statement is executed using the updateAll() wrapper function

![image-20230721123532929](https://s2.loli.net/2023/07/21/joV8dIY432MmGfD.png)
