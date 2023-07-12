# ibos oa v4.5.5 SQL注入

SQL injection vulnerability exists in ibos oa v4.5.5

official website:http://www.ibos.com.cn/

version:4.5.5



Function point: Integrated office = "Recruitment management" = "Status" = "Interview"

![image-20230712221927907](https://s2.loli.net/2023/07/12/JrXETLIkOYu3dxt.png)

![image-20230712222230307](https://s2.loli.net/2023/07/12/iQ7eKtHdTM2gBvX.png)



Using burpsuite to capture the packet, it returned a json format of information, and found a sql error return



![image-20230712222517985](https://s2.loli.net/2023/07/12/FaenjfCZR3l78bq.png)



Save the POST package and use sqlmap for sql injection

<img src="https://s2.loli.net/2023/07/12/J5zH2BWbPoRVFMh.png" alt="image-20230712222752008" style="zoom:50%;" />

![image-20230712222856037](https://s2.loli.net/2023/07/12/ThEFp6uiVWQA3eq.png)

Finally，success！



