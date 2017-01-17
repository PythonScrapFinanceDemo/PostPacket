1.要解决的问题

      http://spds.qhrb.com.cn/SP10/SPOverSee1.aspx

      从比赛指定的网站上抓取信息.产生一个数据文件.获取的信息要完整，包括所有的"参赛者"和所有的日期.除了网页上的列之外(例如排名,客户昵称等),数据集还应包含三个变量:交易日期,排行榜类型,客户代码.

2.解决问题的思路

将该问题分解为两部分:

(1)爬虫部分

          流程:发送post报文,获得返回的响应报文,解析响应报文中的html结构，获得所需要的数据存入csv文件.
   
(2)数据处理部分

数据合并

          流程:
               1.分别合并前十个排行榜类型的2016-04-01到2016-09-30的所有数据,得到十个csv文件,对应"轻量级组","重量级组"......"净利润"
               2.将上一步的十个文件合并一个总的csv文件

生成客户代码

          流程:
               1.得到不重复的客户昵称
               2.根据回撤率和排名将生成唯一标识的客户代码

3.功能描述

(1)爬虫部分

        post报文类型:
                
                    发送十种不同的post报文,分别对应排行榜上的前十个类型,"轻量级组","重量级组","基金组"......"能源化工","净利润".
        
        多线程工作方式:
           
                    采用多线程的方式，且线程数量始终具体日期的网页的页数一致.
        
                    比如:轻量级组的2016-04-01有133页,程序会创建并开启133个线程，同时爬取从第1页到133页的数据
         
        文件存储:
        
                    一个线程写到一个csv文件中,文件命名格式为"排行榜-交易日期-第几页".
        
                    同一个组的所有文件放在一个文件夹下,文件夹以该排行榜的汉语拼音命名,方便归类和查看.
        
                    比如:轻量级组的2016-04-01有133页,那么会在"QingLiangZu"文件夹下存储为133个csv文件,分别是"QingLiangZu-2016-04-01-1","QingLiangZu-2016-04-01-2"......"QingLiangZu-2016-04-01-133".
                           
                    最终,轻量级组的2016-04-01到2016-09-30的所有文件存储在"QingLiangZu"文件夹下.
        
(2)数据处理部分

数据合并：

        分批次合并数据文件,csv文件列标题排序方式,如下:
['客户昵称','组别','排行榜','时间','排名','当日权益','风险度(%)','净利润','净利润得分','回撤率(%)','回撤率得分','日净值','累计净值',
                    '净值得分','综合得分','参考收益率(%)','指定交易商','操作指导','账户评估']        

生成客户代码：

        检索客户昵称,得到一个不重复的客户昵称列表
        根据回撤率和排名将生成唯一标识的客户代码



4.项目文件结构  


(1)爬虫部分   

  爬虫启动方法: 直接运行Main.py文件,自动完成所有爬取和存储工作


  说明:一共7个文件(按依赖从简单到复杂排序)

  1---date.py  
  
  依赖文件:无
 
        tick_weekend(date_list):
    
                                功能:date_list(剔除周六,周日)      
                                
                                输入:一个日期列表
                            
                                返回:一个日期列表(排除周六,周日)
    
    
        get_date_list(begin_date,end_date):
    
                                功能:调用tick_weekend(),获取交易日期       
                                
                                输入:begin_date(开始日期),end_date(结束日期)
                            
                                返回:该时间范围内的交易日期(排除周六,周日,法定节假日)
                

  2---write.py   

  依赖文件:无

        get_plain_text(ResultSet):
        
                                功能:将BeautifulSoup解析得到的标题对象转换为一个列表
                            
                                输入:ResultSet(BeautifulSoup解析得到的标题对象)
                                
                                返回:一个包含网页中所有列标题的列表
            
            
        select_data(page_source,Date,GroupType):
            
                                功能:调用get_plain_text(),将html解析后写入csv文件    
                            
                                输入:page_source(html源码),Date(交易日期),GroupType(某个排行榜类型)
                                
                                返回:"存储成功"


  3---postpacketpayload.py 

  依赖文件:无
    
        getGroupPayload(data,Date,GroupType):
    
                                功能:构造前十个排行榜类型对应的十种post报文的payload
                                
                                输入:data(第几页),Date(交易日期),GroupType(某个排行榜类型)
                            
                                返回:该排行榜类型对应的post报文的内容payload
            
            
        getGroupHeaders(GroupType):
            
                                功能:构造前十个排行榜类型对应的十种post报文的headers
                                
                                输入:GroupType(某个排行榜类型) 
                            
                                返回:该排行榜类型对应的post报文的内容headers


  4---pagenumber.py 

  依赖文件:3---postpacketpayload.py 

        getOneDayFirstPage(Date,GroupType,WantedPage):
    
                                功能:调用getGroupPayload(),获取某排行榜类型的某交易日期的某一页的html
                            
                                输入:Date(交易日期),GroupType(某个排行榜类型),WantedPage(第几页)
                            
                                返回:GroupType类型的Date交易日期的第WantedPage页的html
                            
            
        getOneDayTotalPageNumber(Date,GroupType):
            
                                功能:调用getOneDayFirstPage(),获取某排行榜类型的某交易日期的网页数量
                            
                                输入:Date(交易日期),GroupType(某个排行榜类型)
                            
                                返回:该排行榜类型在该交易日期的网页数量
                            
                                比如:轻量级组的2016-04-01有133页,则返回133.
                            
                                     输入:2016-04-01,QingLiangJiZu
                                
                                     返回:133

  5---Threading.py 

  依赖文件:2---write.py,3---postpacketpayload.py,4---pagenumber.py 

  
        process_data(threadName,Date,GroupType):
        
                                功能:针对某个排行榜类型的某交易日期的某一页,完成所有的爬取和存储的所有工作
                            
                                输入:线程名(threadName),Date(交易日期),GroupType(某个排行榜类型)
                            
                                返回:None
                            
        class myThread (threading.Thread):
                
                                功能:调用process_data(),自定义线程类
                                
                                参数包括:threadID(线程标识),name(线程名),Date(交易日期),GroupType(某个排行榜类型)



  6---OneGroupMain.py 

  依赖文件:1---date.py,4---pagenumber.py,5---Threading.py 
    
        GetOneGroup(GroupType):
    
                                功能:爬取和存储某个排行榜类型的所有交易日期的所有网页数据
                                
                                     即针对某个排行榜类型,完成所有爬取和存储的所有工作
                            
                                输入:GroupType(某个排行榜类型)
                            
                                返回:None
                            
                                比如:输入QingLiangJiZu(轻量级组),则会在QingLiangJiZu文件夹得到轻量级组2016-04-01到2016-09-30的所有数据

  7---Main.py  

  依赖文件:6---OneGroupMain.py 
        
        main():
        
                                功能:爬取和存储某所有排行榜类型的所有交易日期的所有网页数据
  


(2)数据处理部分   

1----数据合并：

  数据合并启动方法: 直接运行py文件,自动完成所有数据合并工作
  
  说明:仅一个deal_csv_OK.py文件



        get_date(filename):
        
                                功能:将文件名转换为交易日期
                            
                                输入:filename(csv文件名)
                                
                                返回:该文件对应的交易日期
            
            
        deal_csv(folderName,label):
            
                                功能:合并一个文件夹下的所有csv文件,适用于"轻量级组"..."净利润"十个文件夹   
                            
                                输入:folderName(文件夹名字),label(标志,如果是前四组,默认label=0,如果是后六组,label=1)
                                
                                返回:该文件夹下所有csv文件合并后的总的csv文件


        all_to_one(nameList):
        
                                功能:将deal_csv()合并后得到的十个csv文件,再次合并一个包含所有数据的csv文件
                            
                                输入:nameList(想要合并的文件名的列表)
                                
                                返回:namelist中所有csv文件合并后的总的csv文件
            
            
        change_columns_order(columns_list):
            
                                功能:对all_to_one()合并后的csv文件,重新对列进行排序 
                            
                                输入:columns_list(csv文件列标题的列表)
                                
                                返回:列标题被重新排序后的csv文件

        sort_df():
        
                                功能:对change_columns_order()重新排序后的文件按行进行排序
                            
                                输入:空
                                
                                返回:行被重新排序后的csv文件
            

2----生成客户代码:

        make_unique(original_list)():
        
                                功能:获取sort_df()重新行排序后的文件中的客户昵称,得到一个不重复的客户昵称列表
                            
                                输入:original_list(客户昵称列表)
                                
                                返回:得到一个不重复的客户昵称列表


        get_id():
        
                                功能:
                            
                                输入:空
                                
                                返回: