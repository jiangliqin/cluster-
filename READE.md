1.node server.js来启动服务器，在新的终端访问:curl localhost:3000 模拟客户端的请求；

2.cluster负载均衡策略的测试：
	a.安装siege;
	b.node server.js>server.js;
	c.在终端启动,每秒50个并发请求：sudo siege -c 50 http://localhost:300;
	d.查看分析server.log
	###用R语言分析server.log;
	df<-read.table(file="server.log",skip=9,header=FALSE);
	summary(df)

	###或者用命令行统计负载均衡结果：
	cat server.log|grep  'worker\d'|awk '{a[$1]++} END{for(i in a){print i,a[i]}}'
	结果：
	worker1 680
	worker2 707
	worker3 673
	worker4 685