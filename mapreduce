#Importing Packages for data transformations and multi-threading
import re
import pandas as pd
import threading
import queue


#Defining data cleaning function
def cleanData(file):
    token = []
    #Removing the punctuations  and other irrelevant string content not meant for mapping
    wform = re.compile("[a-z]+")
    for line in file:
        if len(line) > 0:
            token.append(wform.findall(line.lower()))
    token = [x for x in token if x != []]
    #list = [item for i in token for item in i]
    return token


#Defining the data Split function
def split_function(list):
    part = []
    for line in list:
        part.append(line)
    list1 = part[0:5000]
    list2 = part[5001:]
    list3 = [list1,list2]
    return list3
    
#Defining mapper function, two mapper function gets defined here
def mapper1(list,map_q1):
    li = [wordl for i in list for wordl in i]
    mapping = []
    for i in li:
        word = i
        mapping.append("%s\t%d"%(word,1))
    #queuing up the mapper elements
    map_q1.put(mapping)
def mapper2(list,map_q2):
    li = [wordl for i in list for wordl in i]
    mapping = []
    for i in li:
        word = i
        mapping.append("%s\t%d"%(word,1))
    #queuing up the mapper elements
    map_q2.put(mapping)
 

#Defining sort by function
def Sort_function(mapping1,mapping2): 
    mapping = mapping1+mapping2
    mapping.sort()
    return mapping

#Defining partition function
def Partition(tosort):
    a = []
    b = []
    for i in tosort:
        x = re.search("^[a-m]", i)
        if(x):
            a.append(i)
        else:
            b.append(i)
    list = [a,b]
    return list

#Defining reducer function, two reducers gets defined

def Reducer1(list,red_q1):
    cur_word = None
    cur_count = 0
    f_count = {}
    for i in list:
        word,count = i.split('\t',1)
        count = int(count)
        if cur_word == word:
            cur_count += count
        else:
            cur_word = word
            cur_count = count
        f_count[cur_word] = cur_count
    if cur_word == word:
        f_count[cur_word] = cur_count
    #queuing up the elements
    return red_q1.put(f_count)
def Reducer2(list,red_q2):
    cur_word = None
    cur_count = 0
    f_count = {}
    for i in list:
        word,count = i.split('\t',1)
        count = int(count)
        if cur_word == word:
            cur_count += count
        else:
            cur_word = word
            cur_count = count
        f_count[cur_word] = cur_count
    if cur_word == word:
        f_count[cur_word] = cur_count
    #queuing up the elements
    return red_q2.put(f_count)

#Performing the big data map reduce using multithreading

def MapReduce(Path):
        map_q1 = queue.Queue()
        map_q2 = queue.Queue()
        red_q1 = queue.Queue()
        red_q2 = queue.Queue()
        file = open (Path,encoding="utf8")
        list1 = cleanData(file)
        list2 = split_function(list1)
        mapping1 = threading.Thread(target=mapper1,args = (list2[0],map_q1))
        mapping2 = threading.Thread(target=mapper2,args =(list2[1],map_q2))
        mapping1.start()
        mapping2.start()
        mapping1.join() 
        mapping2.join() 
        #mapping1 = mapper1(list2[0])
        #mapping2 = mapper2(list2[1])
        mapping1= []
        for i in map_q1.get():
            mapping1.append(i)
        mapping2=[]
        for j in map_q2.get():
            mapping2.append(j)
        tosort = Sort_function(mapping1,mapping2)
        Part = Partition(tosort)
        Reduce1 = threading.Thread(target = Reducer1,args =(Part[0],red_q1))
        Reduce2 = threading.Thread(target = Reducer2,args =(Part[1],red_q2))
        Reduce1.start()
        Reduce2.start()
        Reduce1.join()
        Reduce2.join()
        #Reduce1 = Reducer1(Part[0])
        #Reduce2 = Reducer2(Part[1])
        Reduce1 = red_q1.get()
        Reduce2 = red_q2.get()
        Reduce1.update(Reduce2)
        Output_df = Reduce1
        Output_df = pd.DataFrame(Output_df.items(), columns=['Word', 'Count'])
        Output_df.to_csv(r'C:\\Users\\skota\\Desktop\\backup\\big_data\\bigdata_output.csv')
        return Output_df



#Mention the path of the file here,

MapReduce(Path=' ') 
