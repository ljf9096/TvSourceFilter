main.py依次运行modules中6个模块。1：捕获信号源。从 config/channels.txt 捕获信号源并保存到 output/ownsource.txt。2：组合信号源。从多个渠道config中收集直播源：网络订阅源（subscribe.txt）,本地用户源（user_result.txt）,本地源文件（localsource.txt，已收入很多Y）,自有源（ownsource.txt）合并多个信号源文件。输出合并结果netsource.txt - 纯网络源，allsource.txt - 所有源。3：清理、过滤无效的信号源。去除重复、无效的链接。读取输入文件 output/allsource.txt，从 config/blacklist.txt 读取黑名单过滤，输出 output/allsourcecleaned.txt。4：拆分信号源。将合并后的信号源按频道分类。扫描 allsourcecleaned.txt 并统一频道名称，每个标准频道保存为一个独立的txt文件，路径：output/channels/频道名称.txt，配置文件示例，config/othernames.txt。5：优选频道信号源。基于速度、稳定性等指标。从 config/whitelist.txt 读取白名单关键词并加载，对每个频道的源文件进行独立筛选，输入：output/channels/频道名称.txt，输出：output/channels/频道名称_picked.txt。6：替换频道列表，生成可用频道文件。读取用户模板，"config", "user_demo.txt"，输入模板 (config/user_demo.txt)，优选源文件 (output/channels/CCTV-1_picked.txt)，输出结果 (output/new_result.txt)。
## 电视源抓取及清理项目
#### config文件夹

blacklist:源网址中包含字符串黑名单文件，#开头行为注释

whitelist: 源网址中包含字符串白名单文件，#开头行为注释

channels: 周一三五日上午自动运行会按此文件中单行抓取频道源，#开头行为注释

localsource：可自定义一些用户用过的频道源，用于总源收集，#开头行为注释

user_result：类同于localsource.txt，用于总源收集，#开头行为注释

othernames：设置处理频道别名，每个想获取的频道都建议做一个别名，#开头行为注释

subscribe: 其他来源网络源路径配置，#开头行为注释

user_demo：用户想配置的直播源文件样板

#### output文件夹

allsource: 源网址总集-自动生成

allsourcecleaned: 根据黑名单筛选后的源网址总集-自动生成

netsource：根据配置的subscribe文件自动合成源网址总集

ownsource：根据配置的channels文件自动抓取源网址总集

new_result：根据user_demo自动从channels各picked文件来生成的自定义直播源

channels文件夹：根据othernames处理的各频道源，_picked为白名单筛选

生成源可配合fork的Guovin大佬的项目使用
