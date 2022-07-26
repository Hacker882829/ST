
1

#include<iostream>
#include<fstream>
#include<sstream>
#include<string>
using namespace std;
class student
{
public:
string usn,name,branch,buffer;
void read();
void pack();
void write();
void unpack();
int search(string);
void modify(string);
};
int main()
{
int choice,i;
student s;
string key;
fstream file;
file.open("2.txt",ios::out|ios::app);
file.close();
while(1)
{
cout<<"\n1.add record 2.modify 3.search 4.exit\n";
cout<<"enter ur choice:";
cin>>choice;
switch(choice)
{
case 1:
break;
cout<<"data:";
s.read();
s.pack();
s.write();
case 2:cout<<"enter the usn\n";
cin>>key;
s.modify(key);
break;
case 3:cout<<"enter the usn\n";
cin>>key;
i=s.search(key);
break;
default:exit(0);
} //end of switch
} //end of while
return 0;
}
void student::read( ) //reads student data from key board
{
cout<<"usn:";
cin>>usn;
cout<<"name:";
cin>>name;
cout<<"branch:";
cin>>branch;
}
void student::pack()
{
buffer.erase();
buffer=usn+'|'+name+'|'+branch; //packing student attribute into buffer
for(;buffer.size()<100;) //making buffer size 100
buffer+='$';
buffer+='\n'; //ending record with \n•
}
void student::write()
{
fstream file;
file.open("2.txt",ios::out|ios::app);
file<<buffer; //writing record into file
file.close();
}
int student::search(string key) //returns -1 or position of next record
{
fstream file;
int flag=0,pos=-1;
file.open("2.txt",ios::in);
while(!file.eof())
{
buffer.erase(); //erasing any previous contents in buffer
getline(file,buffer);
unpack();
if(key==usn)
{
flag=1;

cout<<"\nfound,the record is:\n"<<buffer;
pos=file.tellg(); //gets address of next record
pos=pos-(buffer.size()+1); //gets address of found
record
break;
}
}
if(!flag)
cout<<"record not found";
file.close();
return pos;
}
void student::unpack()
{
string sem;
int ch=1,i=0;
usn.erase();
while(buffer[i]!='|')
usn+=buffer[i++];
name.erase();
i++;
while(buffer[i]!='|')
name+=buffer[i++];
branch.erase();
i++;
while(buffer[i]!='$')
branch+=buffer[i++];
}
void student::modify(string key)
{
int choice,pos;
fstream file;
pos=search(key);
if(pos>=0)
{
cout<<"\n want to modify?\n1. USN 2.Name 3.Branch (enter ur choice)...";
cin>>choice;
switch(choice)
{
case 1:cout<<"usn:";
cin>>usn;
break;
case 2:cout<<"name:";
cin>>name;
break;
case 3:cout<<"branch:";
cin>>branch;
break;
default:cout<<"wrong choice";
}
buffer.erase();
pack();
file.open("2.txt");
file.seekp(pos,ios::beg); //moving p pointer to the begining of the deleted
record
file<<buffer; //writing record into file
file.close();
cout<<"\n modification successful\n";
}
else
cout<<"\n modification unsuccessful\n";
}



3




#include<iostream>
#include<fstream>
#include<sstream>
#include<string>
using namespace std;
class student
{
public:
string usn,name,branch,buffer;
void read();
void pack();
void write();
void unpack();
void search(string);
void modify(string);
};
int main()
{
int choice,i;
student s;
string key;
fstream file;
file.open("3.txt",ios::out|ios::app);
file.close();
while(1)
{
cout<<"\n1.add record 2.modify 3.search 4.exit\n";
cout<<"enter ur choice:";
cin>>choice;
switch(choice)
{
case 1:
break;
cout<<"data:";
s.read();
s.pack();
s.write();
case 2:cout<<"enter the usn\n";
cin>>key;
s.modify(key);
break;
case 3:cout<<"enter the usn\n";
cin>>key;
s.search(key);
break;
default:exit(0);
}
}
return 0;
}
void student::read( ) //reads student data from key board
{
cout<<"usn:";
cin>>usn;
cout<<"name:";
cin>>name;
cout<<"branch:";
cin>>branch;
}
void student::pack()
{
buffer.erase();
buffer=usn+'|'+name+'|'+branch+'$'+'\n'; //packing student attribute into buffer
}
void student::write()
{
fstream file;
file.open("3.txt",ios::out|ios::app);
file<<buffer;
file.close();
}
void student::search(string key)
{
fstream file;
int flag=0,pos=-1;
file.open("3.txt",ios::in);
while(!file.eof())
{
buffer.erase(); //erasing any previous contents in buffer
getline(file,buffer);
unpack();
if(key==usn)
{
flag=1;
cout<<"\nfound,the record is:\n"<<buffer;
break;
}
}
if(!flag)
cout<<"record not found";
file.close();
void student::unpack()
{
int ch=1,i=0;
usn.erase();
while(buffer[i]!='|')
usn+=buffer[i++];
name.erase();
i++;
while(buffer[i]!='|')
name+=buffer[i++];
branch.erase();
i++;
while(buffer[i]!='$')
branch+=buffer[i++];
}
void student::modify(string key )
{
fstream file,fnew;
int choice,flag=0;
file.open("3.txt",ios::in);
fnew.open("temp.txt",ios::out);
while(!file.eof())
{
buffer.erase(); //erasing any previous contents in buffer
getline(file,buffer);
if(buffer.empty())
continue;
unpack();
if(key==usn)
{
flag=1;
cout<<"\nfound,the record is:\n"<<buffer;
cout<<"\n want to modify?\n1. USN 2.Name 3.Branch (enter ur choice)...";
cin>>choice;
switch(choice)
{
case 1:cout<<"usn:";
cin>>usn;
break;
case 2:cout<<"name:";
cin>>name;
break;
case 3:cout<<"branch:";
cin>>branch;
break;
default:cout<<"wrong choice";
}
}
pack();
fnew<<buffer;
}
if (!flag)
cout<<"\nStudent not found!!!\n";
file.close( );
fnew.close();
remove("3.txt");
rename("temp.txt","3.txt");
remove("temp.txt");
}



4




#include<iostream>
#include<sstream>
#include<fstream>
#include<string>
using namespace std;
class student
{
public:string usn,name,branch,buffer;
int count,rrn_list[100]; //array to store address of records
void read();
void write();
void pack();
void create_rrn();
void search_by_rrn(int);
};
void student::read()
{
cout<<"usn";
cin>>usn;
cout<<"name";
cin>>name;
cout<<"branch";
cin>>branch;
}
void student::pack()
{
buffer.erase();
buffer=usn+'|'+name+'|'+branch +'$'+'\n'; //variable length record
}
void student::write()
{
int pos;
fstream file;
file.open("4.txt",ios::out|ios::app);
pos=file.tellp(); //getting the address where the new record is to be written
file<<buffer;
file.close();
rrn_list[++count]=pos; //storing address of the record in array
}
void student::create_rrn() //initializes the array rrn_list for existing records
{
fstream file;
int pos=-1;
count=0;
file.open("4.txt",ios::in);
while(!file.eof())
{
pos=file.tellg();
buffer.erase();
getline(file,buffer);
if(buffer.empty())continue;
rrn_list[++count]=pos;
}
file.close();
}
void student::search_by_rrn(int rrn)
{
int pos=-1;
fstream file;
if(rrn>count || rrn<1)
cout<<"record not found\n";
else
{
buffer.erase();
file.open("4.txt",ios::in);
pos=rrn_list[rrn];
file.seekg(pos,ios::beg);
getline(file,buffer);
cout<<"\nrecord is..."<<buffer<<"\n";
}
}
int main()
{
int ch,rrn;
student s;
fstream file;
file.open("4.txt",ios::out|ios::app);
file.close();
s.create_rrn();
while(1)
{
cout<<"\n1.add 2.search 3.exit\n enter your choice:";
cin>>ch;
switch(ch)
{
case 1:cout<<"enter data\n";
s.read();
s.pack();
s.write();
case 2:cout<<"enter the rrn\n";
cin>>rrn;
s.search_by_rrn(rrn);
break;
default:exit(0);
}
}
return 0;
}




5




#include<iostream>
#include<sstream>
#include<fstream>
#include<string>
using namespace std;
class primary_index
{
public:
string usn,name,branch,buffer;
string usn_list[100]; //to store usn
int address_list[100],count,pos; / / to store address of respective usn
primary_index();
void insert();
void remove(string);
void search(string);
int search_primary_index(string);
void extract_usn_pos();
~primary_index();
};
primary_index::primary_index() //initializing the address and usn array
{
fstream file;
count=-1;
file.open("index.txt",ios::out|ios::app);
file.close();
file.open("index.txt",ios::in);
while(!file.eof())
{
pos=file.tellg();
buffer.erase();
getline(file,buffer);
if(buffer.empty()) continue;
extract_usn_pos();
++count;
usn_list[count]=usn;
address_list[count]=pos;
}
file.close();
}
int primary_index::search_primary_index(string key) //using linear search to search the array
{
int i;
for(i=0;i<=count;i++)
{
if(usn_list[i]==key)
return i;
}
return -1;
}
void primary_index::insert() //inserts record into file and also adds address and usn in respective arrays
{
int i;
string sem;
fstream file;
cout<<"\nusn:";
cin>>usn;
i=search_primary_index(usn);
if(i>=0)
{
cout<<"\n USN exists...primary key violation\n";
}
else
{
cout<<"\nname:";
cin>>name;
cout<<"\nbranch:";
cin>>branch;
buffer.erase();
buffer=usn+'|'+name+'|'+branch+'$'+'\n';
file.open("5.txt",ios::out|ios::app);
pos=file.tellp(); //getting address before record is written
file<<buffer;
file.close();
count++;
usn_list[count]=usn;
address_list[count]=pos;
}
}
void primary_index::search(string key) //searching in file
{
int i,address;
fstream file;
buffer.erase();
i=search_primary_index(key)
if(i>=0)
{
file.open("5.txt",ios::in);
address=address_list[i];
file.seekg(address,ios::beg);
getline(file,buffer);
cout<<"record found...\n"<<buffer;
file.close();
}
else
cout<<"record not found\n";
}
void primary_index::remove(string key)
{
int address,i,j;
fstream file;
j=search_primary_index(key);
if(j>=0)
{
for(i=j;i<count;i++) //removing entries in the array also
{
usn_list[i]=usn_list[i+1];
address_list[i]=address_list[i+1];
}
count--;
cout<<"record deleted";
}
else
cout<<"record to be deleted is not found";
}
void primary_index::extract_usn_pos() //unpacikg only usn
{
string st_pos;
int i=0;
usn.erase();
while(buffer[i]!='|')
usn+=buffer[i++];
i++;
st_pos.erase();
while(buffer[i]!='$')
st_pos+=buffer[i++];
istringstream out(st_pos);
out>>pos;
}
primary_index::~primary_index()
{
int i;
string st_pos;
fstream file;
file.open("index.txt",ios::out);
for(i=0;i<=count;i++) {
stringstream out;
out<<address_list[i];
st_pos=out.str();
buffer.erase();
buffer=usn_list[i]+'|'+st_pos+'$'+'
\n';
file<<buffer;
}
file.close();
}
int main() {
int ch,flag=0;
string key;
primary_index i1;
fstream file;
file.open("5.txt",ios::out|ios::app);
file.close();
while(flag!=1) {
cout<<"
\n1.add 2.search 3.delete 4.exit
\n";
cout<<"enter your choice:";
cin>>ch;
switch(ch) {
case 1:cout<<"enter the data";
i1.insert();
break;
case 2:cout<<"
\nenter the usn to be searched:";
cin>>key;
i1.search(key);
break;
case 3:cout<<"
\nenter the usn to be deleted";
cin>>key;
i1.remove(key);
break;
default: flag=1;break;
}
}
return 0;
}



6



#include<iostream>
#include<sstream>
#include<fstream>
#include<string>
using namespace std;
class secondary_index
{
public:
string usn,name,branch,buffer;
string name_list[100]; //to store name
int address_list[100],count,pos; // to store address of respective name
secondary_index();
void insert();
void remove(string);
void search(string);
int search_secondary_index(string);
void extract_name_pos();
void sort_index();
~secondary_index();
};
secondary_index::secondary_index() //initializing the address and usn array
{
fstream file;
count=-1;
file.open("s_index.txt",ios::out|ios::app);
file.close();
file.open("s_index.txt",ios::in);
while(!file.eof())
{
pos=file.tellg();
buffer.erase();
getline(file,buffer);
if(buffer.empty()) continue;
extract_name_pos();
++count;
name_list[count]=name;
address_list[count]=pos;
}
file.close();
}
int secondary_index::search_secondary_index(string key)
{
int i;
for(i=0;i<=count;i++)
{
if(name_list[i]==key)
return i;
}
return -1;
}
void secondary_index::insert() //inserts record into file and also adds address and usn in respective
arrays
{
int i;
string sem;
fstream file;
cout<<"\nusn:";
cin>>usn;
cout<<"\nname:";
cin>>name;
cout<<"\nbranch:";
cin>>branch;
buffer.erase();
buffer=usn+'|'+name+'|'+branch+'$'+'\n';
file.open("6.txt",ios::out|ios::app);
pos=file.tellp(); //getting address before record is written
file<<buffer;
file.close();
count++;
name_list[count]=name;
address_list[count]=pos;
sort_index();
}
void secondary_index::sort_index() //to arrays when a new record is added
{
int i,j,temp;
string temp_name;
for(i=0;i<count;i++)
{
for(j=i+1;j<=count;j++)
{
if(name_list[i]>name_list[j])
{
temp_name=name_list[i];
name_list[i]=name_list[j];
name_list[j]=temp_name;
temp=address_list[i];
address_list[i]=address_list[j];
address_list[j]=temp;
}
}
}
}
void secondary_index::search(string key) //searching in file
{
int i,address,flag=0;
fstream file;
buffer.erase();
i=search_secondary_index(key);
while(i>=0 && name_list[i]==key)
{
flag=1;
file.open("6.txt",ios::in);
address=address_list[i];
file.seekg(address,ios::beg);
getline(file,buffer);
cout<<"\nrecord found..."<<buffer;
file.close();
i++;
}
if(!flag)
cout<<"record not found\n";
}
void secondary_index::remove(string key)
{
int address,i,j,flag=0;
fstream file;
j=search_secondary_index(key);
while(j>=0 && name_list[j]==key) //while loop to delete repeated names
{
flag=1;
for(i=j;i<=count;i++) //removing entries in the array only
{
name_list[i]=name_list[i+1];
address_list[i]=address_list[i+1];
}
count--;
cout<<"\n record deleted";
}
if(!flag)
cout<<"\n record to be deleted is not found";
}
void secondary_index::extract_name_pos() //unpacking only usn
{
string st_pos;
int i=0;
name.erase();
while(buffer[i]!='|')
name+=buffer[i++];
i++;
st_pos.erase();
while(buffer[i]!='$')
st_pos+=buffer[i++];
istringstream out(st_pos);
out>>pos;
}
secondary_index::~secondary_index()
{
int i;
string st_pos;
fstream file;
file.open("s_index.txt",ios::out);
for(i=0;i<=count;i++)
{
stringstream out;
out<<address_list[i];
st_pos=out.str();
buffer.erase();
buffer=name_list[i]+'|'+st_pos+'$'+'\n';
file<<buffer;
}
file.close();
}
int main()
{
int ch,flag=0;
string key;
secondary_index i1;
fstream file;
file.open("6.txt",ios::out|ios::app);
file.close();
while(flag!=1)
{
cout<<"\n1.add 2.search 3.delete 4.exit\n";
cout<<"enter your choice:";
cin>>ch;
switch(ch)
{
case 1:cout<<"enter the data";
i1.insert();
break;
case 2:cout<<"\nenter the name to be searched:";
cin>>key;
i1.search(key);
break;
case 3:cout<<"\nenter the name to be deleted:";
cin>>key;
i1.remove(key);
break;
default: flag=1;break;
}
}
return 0;
}




7




#include<iostream>
#include<fstream>
#include<string>
using namespace std;
class coseq
{
public:
string list1[100],list2[100]; //two lists
int count1,count2; // two counters
void load_list();
void sort_list();
void match();
};
void coseq::load_list() //loads contents of files into respective lists
{
fstream file1,file2;
string name;
count1=-1;
count2=-1
file1.open("71.txt"); //reading from 1
st file
while(!file1.eof())
{
name.erase();
getline(file1,name);
list1[++count1]=name;
}
file1.close();
cout<<"names is 1st file\n";
for(int i=0;i<=count1;i++)
cout<<list1[i]<<"\n";
file2.open("72.txt"); //reading from 2
nd file
while(!file2.eof())
{
name.erase();
getline(file2,name);
list2[++count2]=name;
}
file2.close();
cout<<"names in 2nd file\n";
for(int i=0;i<=count2;i++)
cout<<list2[i]<<"\n";
}
void coseq::sort_list() //sorting both list
{
int i,j;
string temp;
for(int i=0;i<=count1;i++)
{
for(int j=i+1;j<=count1;j++)
{
if(list1[i]>list1[j])
{
temp=list1[i];
list1[i]=list1[j];
list1[j]=temp;
}
}
}
for(i=0;i<=count2;i++)
{
for(j=i+1;j<=count2;j++)
{
if(list2[i]>list2[j])
{
temp=list2[i];
list2[i]=list2[j];
list2[j]=temp;
}
}
}
cout<<"\nafter sorting\n";
cout<<"names of 1st file: \n";
for(int i=0;i<=count1;i++)
cout<<list1[i]<<"\n";
cout<<"\n names of 2nd file: \n";
for(int i=0;i<=count2;i++)
cout<<list2[i]<<"\n";
}
void coseq::match() //intersecting two list
{
int i=0,j=0;
cout<<"\n common names are: ";
while(i<=count1 && j<=count2)
{
if(list1[i]==list2[j])
{
if(list1[i-1]!=list1[i]) // avoiding repeated names
cout<<list1[i]<<"\n";
i++; 
j++;
}
if(list1[i]<list2[j]) i++;
if(list1[i]>list2[j]) j++;
}
}
int main()
{
coseq c;
c.load_list();
c.sort_list();
c.match();
return 0;
}






8






#include <iostream>
#include <fstream>
#include <string>
using namespace std;
class coseq
{
public:
string list[10][100];
string outlist[100];
int count[10];
int current[10];
void load_list();
void read_file(int);
void sort_list(int);
void merge();
};
void coseq::read_file(int i)
{
fstream file;
string name;
switch(i)
{
case 1: file.open("name1.txt");break;
case 2: file.open("name2.txt");break;
case 3: file.open("name3.txt");break;
case 4: file.open("name4.txt");break;
case 5: file.open("name5.txt");break;
case 6: file.open("name6.txt");break;
case 7: file.open("name7.txt");break;
case 8: file.open("name8.txt");break;
}
while (!file.eof())
{
name.erase();
getline(file,name);
if(name.length()!=0)
list[i][++count[i]]=name;
}
file.close( );
cout<<"
\
n content of file: "<<i;
for(int j=0;j<=count[i];j++)
cout<<"
\n"<<list[i][j];
}
void coseq::load_list() {
for (int i=1;i<=8;i++) {
count[i]=
-1;
read_file(i);
sort_list(i);
}
}
void coseq::sort_list(int k) {
int i,j;
string temp;
for (i=0;i<=count[k];i++) {
for (j=i+1;j<=count[k];j++) {
if (list[k][i]>list[k][j]) {
temp=list[k][i];
list[k][i]=list[k][j];
list[k][j]=temp;
}
}
}
cout<<"
\
n after sorting file: "<<k;
for(int j=0;j<=count[k];j++)
cout<<"
\n"<<list[k][j];
}
void coseq::merge() {
string smallest;
int small_list, t=
-1,start=1,avail[9],avail_lists=8;
for (int i=1;i<=8;i++) 
{
avail[i]=1;
current[i]=0;
}
while (avail_lists>1)
{
if (!avail[start])
{
start++;
continue;
}
small_list=start;
smallest=list[start][current[start]];
for (int i=start+1;i<=8;i++)
{
if (!avail[i]) continue;
if (list[i][current[i]]<smallest)
{
smallest=list[i][current[i]];
small_list=i;
}
}
current[small_list]++;
if (current[small_list]>count[small_list])
{
avail[small_list]=0;
avail_lists--;
}
outlist[++t]=smallest;
for (int j=1;j<=8;j++) //for loop to eliminate repeated element
{
while(list[j][current[j]]==smallest && current[j]<=count[j])
{
}
}
}//end of while
current[j]++;
if (current[j]>count[j])
{
avail[j]=0;
avail_lists--;
break;
}
for (int i=1;i<=8;i++) //while loop terminates when there is only 1 list left, that has to copied to
output list
if (avail[i])
{
for (int j=current[i];j<=count[i];j++)
{
if(outlist[t]!=list[i][j]) //eliminating repeated elements
outlist[++t]=list[i][j];
}
}
cout<<"\nThe Merged List:";
for (int i=0;i<=t+1;i++)
cout<<"\n"<<outlist[i];
}
int main()
{
coseq c1;
c1.load_list();
c1.merge();
return 0;
}
