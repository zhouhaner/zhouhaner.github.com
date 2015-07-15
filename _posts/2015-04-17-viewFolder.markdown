---
layout: post
title: "如何遍历一个文件夹中所有文件" 
comments: true
share: true
tags: 笔记
---


C/C++本身并没有处理文件夹的函数（linux下有，windows下无），但是编译器提供处理文件夹函数。

**解决方案1:**

用DOS命令 DIR 并转向到一个文件，再打开文件读出一个一个文件名。

例如：
	
	#include <stdio.h>
	#include <windows.h>
	
	int main()
	{
		char cmd[80] = "DIR/B/S C:\\Users\\Joway\\1 > fileName.txt";
		system(cmd);
		FILE *fileNameTxt=fopen("fileName.txt","r");
		
		//do something
		//可从文件中一行行读取文件名，但是其中也包括了目录的名字
		//所以得判断能不能打开fopen 
	
		remove("fileName.txt");
		return 0;
	}

你就获得C:\\Users\\Joway\\1 文件夹中及其子文件夹内的所有文件，选项意思是 只列 文件名和扩展名(/b)，对当前文件夹及其子文件夹所有内容列表(/s)。

并存入文件 fileName.txt 

接着，你可以 用FILE *fileNameTxt=fopen("fileName.txt","r");

打开文件

用 fgets() 读文件名。


----------

**解决方案 2:**


缺点：

1. 只能遍历该文件下直接存在的文件，若文件夹目录下还有文件夹，则不能遍历到，会当作是一个空文件！

2. 只能在cpp中使用！！


注意：在C/C++中，可以用“/”或者“\\”来代替路径中的 “\” 。


	#include <stdio.h>
	#include <io.h>


	int main(int argc, char const *argv[])
	{
		_finddata_t fileDir;//是一个结构体，用来保存一个文件信息！
	
		char* dir = "E:/Visual Stdio/批处理文件/Debug/1/*.*";//用来保存路径
		long lfDir;//保存目录的句柄
	
		//在一个路径中找到第一个文件，并把该文件的全名传给fileDir
		//返回一个独一无二的搜索句柄，句柄标识了文件信息
		if ((lfDir = _findfirst(dir, &fileDir)) == -1l)
			printf("No file is found\n");
	
		else{
			//do some thing
	
			while (_findnext(lfDir, &fileDir) == 0){//通过句柄搜索下一个文件
													//并且把文件信息传入fileDir
				printf("%s\n", fileDir.name);//可获得文件名
				printf("%d\n", fileDir.size);//可获得文件大小
	
				// do some things
			}
		}
		_findclose(lfDir);//直接会关闭该文件夹下所有文件
	
		return 0;
	}







----------

**解决方案3:**

用C++代码实现遍历当前目录及其子文件夹下所有文件。但是也会读取到目录本身。(只在windows下可行)


	#include <io.h>  
	#include <fstream>  
	#include <string>  
	#include <vector>  
	#include <iostream>  
	 using namespace std;  
	  
	  
	//获取所有的文件名  
	void GetAllFiles( string path, vector<string>& files)    
	{
	  
	    long   hFile   =   0;    
	    //文件信息    
	    struct _finddata_t fileinfo;    
	    string p;    
	    if((hFile = _findfirst(p.assign(path).append("\\*").c_str(),&fileinfo)) !=  -1)    
	    {    
	        do    
	        {     
	            if((fileinfo.attrib &  _A_SUBDIR))    
	            {    
	                if(strcmp(fileinfo.name,".") != 0  &&  strcmp(fileinfo.name,"..") != 0)    
	                {  
	                    files.push_back(p.assign(path).append("\\").append(fileinfo.name) );  
	                    GetAllFiles( p.assign(path).append("\\").append(fileinfo.name), files );   
	                }  
	            }    
	            else    
	            {    
	                files.push_back(p.assign(path).append("\\").append(fileinfo.name) );    
	            }   
	  
	        }while(_findnext(hFile, &fileinfo)  == 0);    
	  
	        _findclose(hFile);   
	    }   
	  
	}    
	  
	//获取特定格式的文件名  
	void GetAllFormatFiles( string path, vector<string>& files,string format)    
	{    
	    //文件句柄    
	    long   hFile   =   0;    
	    //文件信息    
	    struct _finddata_t fileinfo;    
	    string p;    
	    if((hFile = _findfirst(p.assign(path).append("\\*" + format).c_str(),&fileinfo)) !=  -1)    
	    {    
	        do    
	        {      
	            if((fileinfo.attrib &  _A_SUBDIR))    
	            {    
	                if(strcmp(fileinfo.name,".") != 0  &&  strcmp(fileinfo.name,"..") != 0)    
	                {  
	                    //files.push_back(p.assign(path).append("\\").append(fileinfo.name) );  
	                    GetAllFormatFiles( p.assign(path).append("\\").append(fileinfo.name), files,format);   
	                }  
	            }    
	            else    
	            {    
	                files.push_back(p.assign(path).append("\\").append(fileinfo.name) );    
	            }    
	        }while(_findnext(hFile, &fileinfo)  == 0);    
	  
	        _findclose(hFile);   
	    }   
	}   
	  
	// 该函数有两个参数，第一个为路径字符串(string类型，最好为绝对路径)；  
	// 第二个参数为文件夹与文件名称存储变量(vector类型,引用传递)。  
	// 在主函数中调用格式(并将结果保存在文件"AllFiles.txt"中，第一行为总数)：  
	  
	int main()  
	{  
	    string filePath = "C:\\Users\\Joway\\Desktop\\程序\\批量处理文件\\1";    
	    vector<string> files;    
	    char * distAll = "AllFiles.txt";  
	  
	    //1.0读取所有的文件，包括子文件的文件  
		//GetAllFiles(filePath, files);  
	  
	    //2.0读取所有格式为txt的文件  
	    string format = ".txt";  
		GetAllFormatFiles(filePath, files,format);
		
	    ofstream ofn(distAll);
	    for (int i = 0;i<size;i++)
	    {    
	        ofn<<files[i]<<endl;   
	        cout<< files[i] << endl;  
	    }
	    ofn.close();  
	    return 0;  
	}  

----------



找到一个在系统中调用函数通过资源管理器打开文件夹的方法：

	//打开一个.exe程序就开CMD，输入密码，正确就打开文件夹，错误就关闭CMD。
	
	#include <stdio.h>
	#include <windows.h>
	int main()
	{
		char ch[] = "12345", str[32] = { NULL };
		scanf("%s", str);//密码就是上边的ch保存的12345
		if (strcmp(ch, str) == 0)//密码正确就执行打开
		{
			WinExec("explorer.exe C:\\Windows\\System32", 1);//打开指定文件夹
		}
		else
			return -1;//错误就退出
		return 0;
	}