
####  It split all pcap files in the folder you specify in windows into smaller files containing packets in the size you assign.
#### wireshark and python3 programs must be installed


```python
import os
```

## finds pcap files under the specified folder and assigns them to an array (files_add)


```python
def find_the_way(path,file_format):
    files_add = []
    # r=root, d=directories, f = files
    for r, d, f in os.walk(path):
        for file in f:
            if file_format in file:
                files_add.append(os.path.join(r, file))  
    return files_add
```

## Specify the folder you want processed.


```python
files_add=find_the_way('pcaps','.pcap')
```

## List of pcap files to be processed


```python


print(files_add,"\n\n\n")
print("The folder contains", len(files_add), "pcap file in total" )
```

    ['pcaps\\pcap1.pcap', 'pcaps\\pcap2.pcap'] 
    
    
    
    The folder contains 2 pcap file in total
    

## choice of output size  (How many packets will each file contain?)


```python
piece_size=100000
```

## creates the command and applies it to every file


```python
for ii,i in enumerate (files_add):
    name=i.rfind('\\')
    name=str(i[name+1:])
    new_name="small_"+name
    command='C:/\"Program Files\"/Wireshark/editcap.exe -c '+str(piece_size )+" "+i+" "+new_name
    os.system(command)
    print(ii+1,i, "Done!")
```

    1 pcaps\pcap1.pcap Done!
    2 pcaps\pcap2.pcap Done!
    
