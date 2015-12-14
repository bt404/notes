1. `upstream`用来实现负载均衡策略，通过绑定多个server可以将request根绝设置的策略分配到多个server上。

2. `weight`指定了权重，默认为1，即round-robin将request平均分配到每个server中，设置weight后会根据每台server的weight所占总weight的比重分配相应的request比例。

3. 设置了`backup`的server默认不参与request分配，只在所有非backup机器全不可用时，会访问backup。

4. 设置了`ip_hash`则根据ip来将同一个ip的请求都分配到同一个server上，该选项和weight冲突。该hash的准则是以ipv4点分十进制的前3部分作为key建立hash。`down`配合该指令使用，可以使一台机器暂时不接受request，但是保存hash的现状。

5. 一个请求如果到分配到的server失败，则默认分配到下一个server，只到可用server都不可用，则返回最后一台server返回的错误结果。

6. `max_fails`和`fail_timeout`指定了每个请求访问同一台server允许的失败次数和作为访问失败的超时时间，次数默认为1。

7. `down`可以用来标注一台server暂时不可用（这样就不用删掉代码）。

8. 
