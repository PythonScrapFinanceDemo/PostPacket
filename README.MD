1.Ҫ���������

      http://spds.qhrb.com.cn/SP10/SPOverSee1.aspx

      �ӱ���ָ������վ��ץȡ��Ϣ.����һ�������ļ�.��ȡ����ϢҪ�������������е�"������"�����е�����.������ҳ�ϵ���֮��(��������,�ͻ��ǳƵ�),���ݼ���Ӧ������������:��������,���а�����,�ͻ�����.

2.��������˼·

��������ֽ�Ϊ������:

(1)���沿��

          ����:����post����,��÷��ص���Ӧ����,������Ӧ�����е�html�ṹ���������Ҫ�����ݴ���csv�ļ�.
   
(2)���ݴ�������

���ݺϲ�

          ����:
               1.�ֱ�ϲ�ǰʮ�����а����͵�2016-04-01��2016-09-30����������,�õ�ʮ��csv�ļ�,��Ӧ"��������","��������"......"������"
               2.����һ����ʮ���ļ��ϲ�һ���ܵ�csv�ļ�

���ɿͻ�����

          ����:
               1.�õ����ظ��Ŀͻ��ǳ�
               2.���ݻس��ʺ�����������Ψһ��ʶ�Ŀͻ�����

3.��������

(1)���沿��

        post��������:
                
                    ����ʮ�ֲ�ͬ��post����,�ֱ��Ӧ���а��ϵ�ǰʮ������,"��������","��������","������"......"��Դ����","������".
        
        ���̹߳�����ʽ:
           
                    ���ö��̵߳ķ�ʽ�����߳�����ʼ�վ������ڵ���ҳ��ҳ��һ��.
        
                    ����:���������2016-04-01��133ҳ,����ᴴ��������133���̣߳�ͬʱ��ȡ�ӵ�1ҳ��133ҳ������
         
        �ļ��洢:
        
                    һ���߳�д��һ��csv�ļ���,�ļ�������ʽΪ"���а�-��������-�ڼ�ҳ".
        
                    ͬһ����������ļ�����һ���ļ�����,�ļ����Ը����а�ĺ���ƴ������,�������Ͳ鿴.
        
                    ����:���������2016-04-01��133ҳ,��ô����"QingLiangZu"�ļ����´洢Ϊ133��csv�ļ�,�ֱ���"QingLiangZu-2016-04-01-1","QingLiangZu-2016-04-01-2"......"QingLiangZu-2016-04-01-133".
                           
                    ����,���������2016-04-01��2016-09-30�������ļ��洢��"QingLiangZu"�ļ�����.
        
(2)���ݴ�������

���ݺϲ���

        �����κϲ������ļ�,csv�ļ��б�������ʽ,����:
['�ͻ��ǳ�','���','���а�','ʱ��','����','����Ȩ��','���ն�(%)','������','������÷�','�س���(%)','�س��ʵ÷�','�վ�ֵ','�ۼƾ�ֵ',
                    '��ֵ�÷�','�ۺϵ÷�','�ο�������(%)','ָ��������','����ָ��','�˻�����']        

���ɿͻ����룺

        �����ͻ��ǳ�,�õ�һ�����ظ��Ŀͻ��ǳ��б�
        ���ݻس��ʺ�����������Ψһ��ʶ�Ŀͻ�����



4.��Ŀ�ļ��ṹ  


(1)���沿��   

  ������������: ֱ������Main.py�ļ�,�Զ����������ȡ�ʹ洢����


  ˵��:һ��7���ļ�(�������Ӽ򵥵���������)

  1---date.py  
  
  �����ļ�:��
 
        tick_weekend(date_list):
    
                                ����:date_list(�޳�����,����)      
                                
                                ����:һ�������б�
                            
                                ����:һ�������б�(�ų�����,����)
    
    
        get_date_list(begin_date,end_date):
    
                                ����:����tick_weekend(),��ȡ��������       
                                
                                ����:begin_date(��ʼ����),end_date(��������)
                            
                                ����:��ʱ�䷶Χ�ڵĽ�������(�ų�����,����,�����ڼ���)
                

  2---write.py   

  �����ļ�:��

        get_plain_text(ResultSet):
        
                                ����:��BeautifulSoup�����õ��ı������ת��Ϊһ���б�
                            
                                ����:ResultSet(BeautifulSoup�����õ��ı������)
                                
                                ����:һ��������ҳ�������б�����б�
            
            
        select_data(page_source,Date,GroupType):
            
                                ����:����get_plain_text(),��html������д��csv�ļ�    
                            
                                ����:page_source(htmlԴ��),Date(��������),GroupType(ĳ�����а�����)
                                
                                ����:"�洢�ɹ�"


  3---postpacketpayload.py 

  �����ļ�:��
    
        getGroupPayload(data,Date,GroupType):
    
                                ����:����ǰʮ�����а����Ͷ�Ӧ��ʮ��post���ĵ�payload
                                
                                ����:data(�ڼ�ҳ),Date(��������),GroupType(ĳ�����а�����)
                            
                                ����:�����а����Ͷ�Ӧ��post���ĵ�����payload
            
            
        getGroupHeaders(GroupType):
            
                                ����:����ǰʮ�����а����Ͷ�Ӧ��ʮ��post���ĵ�headers
                                
                                ����:GroupType(ĳ�����а�����) 
                            
                                ����:�����а����Ͷ�Ӧ��post���ĵ�����headers


  4---pagenumber.py 

  �����ļ�:3---postpacketpayload.py 

        getOneDayFirstPage(Date,GroupType,WantedPage):
    
                                ����:����getGroupPayload(),��ȡĳ���а����͵�ĳ�������ڵ�ĳһҳ��html
                            
                                ����:Date(��������),GroupType(ĳ�����а�����),WantedPage(�ڼ�ҳ)
                            
                                ����:GroupType���͵�Date�������ڵĵ�WantedPageҳ��html
                            
            
        getOneDayTotalPageNumber(Date,GroupType):
            
                                ����:����getOneDayFirstPage(),��ȡĳ���а����͵�ĳ�������ڵ���ҳ����
                            
                                ����:Date(��������),GroupType(ĳ�����а�����)
                            
                                ����:�����а������ڸý������ڵ���ҳ����
                            
                                ����:���������2016-04-01��133ҳ,�򷵻�133.
                            
                                     ����:2016-04-01,QingLiangJiZu
                                
                                     ����:133

  5---Threading.py 

  �����ļ�:2---write.py,3---postpacketpayload.py,4---pagenumber.py 

  
        process_data(threadName,Date,GroupType):
        
                                ����:���ĳ�����а����͵�ĳ�������ڵ�ĳһҳ,������е���ȡ�ʹ洢�����й���
                            
                                ����:�߳���(threadName),Date(��������),GroupType(ĳ�����а�����)
                            
                                ����:None
                            
        class myThread (threading.Thread):
                
                                ����:����process_data(),�Զ����߳���
                                
                                ��������:threadID(�̱߳�ʶ),name(�߳���),Date(��������),GroupType(ĳ�����а�����)



  6---OneGroupMain.py 

  �����ļ�:1---date.py,4---pagenumber.py,5---Threading.py 
    
        GetOneGroup(GroupType):
    
                                ����:��ȡ�ʹ洢ĳ�����а����͵����н������ڵ�������ҳ����
                                
                                     �����ĳ�����а�����,���������ȡ�ʹ洢�����й���
                            
                                ����:GroupType(ĳ�����а�����)
                            
                                ����:None
                            
                                ����:����QingLiangJiZu(��������),�����QingLiangJiZu�ļ��еõ���������2016-04-01��2016-09-30����������

  7---Main.py  

  �����ļ�:6---OneGroupMain.py 
        
        main():
        
                                ����:��ȡ�ʹ洢ĳ�������а����͵����н������ڵ�������ҳ����
  


(2)���ݴ�������   

1----���ݺϲ���

  ���ݺϲ���������: ֱ������py�ļ�,�Զ�����������ݺϲ�����
  
  ˵��:��һ��deal_csv_OK.py�ļ�



        get_date(filename):
        
                                ����:���ļ���ת��Ϊ��������
                            
                                ����:filename(csv�ļ���)
                                
                                ����:���ļ���Ӧ�Ľ�������
            
            
        deal_csv(folderName,label):
            
                                ����:�ϲ�һ���ļ����µ�����csv�ļ�,������"��������"..."������"ʮ���ļ���   
                            
                                ����:folderName(�ļ�������),label(��־,�����ǰ����,Ĭ��label=0,����Ǻ�����,label=1)
                                
                                ����:���ļ���������csv�ļ��ϲ�����ܵ�csv�ļ�


        all_to_one(nameList):
        
                                ����:��deal_csv()�ϲ���õ���ʮ��csv�ļ�,�ٴκϲ�һ�������������ݵ�csv�ļ�
                            
                                ����:nameList(��Ҫ�ϲ����ļ������б�)
                                
                                ����:namelist������csv�ļ��ϲ�����ܵ�csv�ļ�
            
            
        change_columns_order(columns_list):
            
                                ����:��all_to_one()�ϲ����csv�ļ�,���¶��н������� 
                            
                                ����:columns_list(csv�ļ��б�����б�)
                                
                                ����:�б��ⱻ����������csv�ļ�

        sort_df():
        
                                ����:��change_columns_order()�����������ļ����н�������
                            
                                ����:��
                                
                                ����:�б�����������csv�ļ�
            

2----���ɿͻ�����:

        make_unique(original_list)():
        
                                ����:��ȡsort_df()�������������ļ��еĿͻ��ǳ�,�õ�һ�����ظ��Ŀͻ��ǳ��б�
                            
                                ����:original_list(�ͻ��ǳ��б�)
                                
                                ����:�õ�һ�����ظ��Ŀͻ��ǳ��б�


        get_id():
        
                                ����:
                            
                                ����:��
                                
                                ����: