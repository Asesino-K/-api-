# -api-
在Ubuntu上调用api出现的代理问题，以clash为例
在开启代理后，会有如下代理变量：
no_proxy=localhost,127.0.0.1,192.168.0.0/16,10.0.0.0/8,172.16.0.0/12,172.29.0.0/16,::1
https_proxy=http://127.0.0.1:7897/
NO_PROXY=localhost,127.0.0.1,192.168.0.0/16,10.0.0.0/8,172.16.0.0/12,172.29.0.0/16,::1
HTTPS_PROXY=http://127.0.0.1:7897/
HTTP_PROXY=http://127.0.0.1:7897/
http_proxy=http://127.0.0.1:7897/
ALL_PROXY=socks://127.0.0.1:7897/
all_proxy=socks://127.0.0.1:7897/

我们把可能会干扰的代理变量删除：
unset ALL_PROXY
unset all_proxy
unset http_proxy
unset https_proxy
unset HTTP_PROXY
unset HTTPS_PROXY
现在再查看代理变量，就只剩下：
no_proxy=localhost,127.0.0.1,192.168.0.0/16,10.0.0.0/8,172.16.0.0/12,172.29.0.0/16,::1
NO_PROXY=localhost,127.0.0.1,192.168.0.0/16,10.0.0.0/8,172.16.0.0/12,172.29.0.0/16,::1
由于调用openai旗下大模型时需要用到代理，所以我们重新加入有效的代理变量：
export HTTP_PROXY="http://127.0.0.1:7897"
export HTTPS_PROXY="http://127.0.0.1:7897"
现在再查看变量，就只剩下干净有效的代理变量了：
no_proxy=localhost,127.0.0.1,192.168.0.0/16,10.0.0.0/8,172.16.0.0/12,172.29.0.0/16,::1
NO_PROXY=localhost,127.0.0.1,192.168.0.0/16,10.0.0.0/8,172.16.0.0/12,172.29.0.0/16,::1
HTTPS_PROXY=http://127.0.0.1:7897
HTTP_PROXY=http://127.0.0.1:7897
注意！！！此方法是一次性的，每开一个新的窗口或者进入一个新的环境，都需要重复执行上述操作。
